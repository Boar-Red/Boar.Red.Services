# 自动构建与依赖更新 / CI and dependency updates

每次 push、Pull Request 或手动运行 Actions，`.github/workflows/ci.yml` 会在 Windows 和 Linux 上还原依赖、执行 Release 构建并显示依赖漏洞报告。可发布的客户端和基础库还会执行 NuGet 打包验证。

Pushes, pull requests and manual Actions runs restore dependencies, build Release and report vulnerable dependencies on Windows and Linux. Publishable libraries also receive a NuGet packaging check.

## 第一次上传后

1. 先把所有被引用的仓库上传到 `Boar-Red` 组织，保留 README 中的仓库和目录名称。当前仓库：`Boar-Red/Boar.Red.Services`。
2. 打开仓库的 **Actions → CI** 查看结果。GitHub 若要求启用 Actions，启用后即可运行；未成功的任务可以在依赖仓库上传后重新运行。
3. 本配置无需填写 NuGet API Key、部署密码或个人 Token，不会提交代码、发布软件包或部署服务。

CI 按兄弟目录布局检出源码：当前仓库使用触发检查的提交或 PR，其他仓库使用各自的公开默认分支。日志中的 **Record source revisions** 记录每个仓库的实际提交，方便复现。跨仓库的变更需先让依赖仓库的默认分支包含兼容代码；正式版本可再把依赖检出版本固定到发布标签或提交。

## 本地运行相同检查

在当前仓库目录执行；需要的兄弟仓库见根目录 README：

```powershell
dotnet restore Boar.Red.Services.slnx
dotnet build Boar.Red.Services.slnx -c Release --no-restore
dotnet test ../Boar.Red.Service/Boar.Red.Service.Test/Boar.Red.Service.Test.csproj -c Release --no-build --no-restore
dotnet test ../Boar.Red.Gateway/Boar.Red.Gateway.Test.Utils/Boar.Red.Gateway.Test.Utils.csproj -c Release --no-build --no-restore
dotnet list Boar.Red.Services.slnx package --vulnerable --include-transitive --no-restore
```

核心库的快速单元测试在两个系统上运行。网关工具测试包含 Windows 可执行文件路径，仅在 Windows 任务中运行。没有对应标准单元测试的宿主只执行构建与依赖检查；缓存控制台测试、需要外部端点的网关集成测试和压力测试需要单独准备环境，不在此 CI 中启动。管理 UI 使用仓库随附的静态产物，CI 不需要闭源 UI 工程。

## 依赖和 SDK

- `global.json` 要求稳定版 .NET 10 SDK，允许使用更高的 .NET 10 feature band；CI 自动安装当前稳定的 10.0.x SDK。
- Dependabot 每周检查 GitHub Actions 和本仓库中实际声明的 NuGet 依赖，通过 PR 提议更新，不会自动合并。NuGet 常规更新暂不跨主版本；聚合仓库自身没有 NuGet 项目，只检查 Actions。
- Actions 固定到完整提交 SHA，Dependabot 可以提议更新。
- 已知的 `Microsoft.Data.SqlClient → System.Security.Cryptography.Pkcs` 传递漏洞暂等待上游更新。还原和审计日志会保留警告；漏洞报告当前用于提示，不会仅因存在漏洞就中断构建，也没有关闭 NuGet 审计。
- 私有部署配置、证书私钥和运行日志受 `.gitignore` 保护，示例配置继续保留。忽略规则不会改变框架的配置加载方式，也不会自动移除已经被 Git 跟踪的文件。

工具说明：[GitHub checkout](https://github.com/actions/checkout)、[setup-dotnet](https://github.com/actions/setup-dotnet)、[Dependabot 配置](https://docs.github.com/en/code-security/reference/supply-chain-security/dependabot-options-reference)。
