# 贡献指南 / Contributing Guide

欢迎参与 Boar.Red 微服务框架的开发！Thank you for your interest in contributing to the Boar.Red microservice framework!

本指南适用于 Boar.Red 全部仓库（[Boar.Red.Service](https://github.com/Boar-Red/Boar.Red.Service) · [Boar.Red.ServiceManager](https://github.com/Boar-Red/Boar.Red.ServiceManager) · [Boar.Red.Gateway](https://github.com/Boar-Red/Boar.Red.Gateway) · [Boar.Red.Cache](https://github.com/Boar-Red/Boar.Red.Cache) · [Boar.Red.Services](https://github.com/Boar-Red/Boar.Red.Services)）。

This guide applies to all Boar.Red repositories.

## 开发环境 / Development Environment

- [.NET 10 SDK](https://dotnet.microsoft.com/)
- Visual Studio 2026 / JetBrains Rider / VS Code（任选 / any of them）

## 源码布局 / Source Layout

各仓库之间使用**相对路径的项目引用**，必须按**兄弟目录**布局 clone，且**目录名不可修改**：

The repos reference each other by relative paths, so they must be cloned as **siblings** with **unchanged directory names**:

```bash
git clone https://github.com/Boar-Red/Boar.Red.Service
git clone https://github.com/Boar-Red/Boar.Red.ServiceManager
git clone https://github.com/Boar-Red/Boar.Red.Gateway
git clone https://github.com/Boar-Red/Boar.Red.Cache
```

## 编码规范 / Coding Style

修改代码前请阅读对应语言的编码规范（IDE 规则见各仓库 `.editorconfig`）：

Please read the coding style guide for the language you are changing (IDE rules live in each repo's `.editorconfig`):

- [C# 编码规范 / C# Coding Style](https://github.com/Boar-Red/Boar.Red.Services/blob/HEAD/docs/csharp-coding-style.md)
- [TypeScript 编码规范 / TypeScript Coding Style](https://github.com/Boar-Red/Boar.Red.Services/blob/HEAD/docs/typescript-coding-style.md)
- [Vue 编码规范 / Vue Coding Style](https://github.com/Boar-Red/Boar.Red.Services/blob/HEAD/docs/vue-coding-style.md)

要点速览 / Highlights：

- 每行不超过 240 字符；`if`/`for`/`while`/`switch` 分支必须使用大括号 / max 240 chars per line; braces are mandatory for control flow blocks.
- 类成员顺序：静态常量 → 静态变量 → 属性 → 类方法 → 私有方法 → 公开方法 → 事件 → 重载 → 接口实现 / class member ordering as documented.
- 模型转换写在源头类型对应的扩展方法中，命名 `To目标类型` / model conversions live in extension methods named `ToTargetType`.
- 异步方法以 `Async` 结尾；接口以 `I` 开头 / async methods end with `Async`; interfaces start with `I`.

## 提交 PR / Submitting a Pull Request

1. Fork 目标仓库并从默认分支创建特性分支 / Fork the target repo and create a feature branch from its default branch.
2. 修改代码，确保可编译；如涉及行为变化，请补充或更新测试 / Make sure it builds; add or update tests for behavior changes.
3. 提交信息使用祈使句、说明"做了什么与为什么" / Use imperative commit messages explaining what & why.
4. 发起 PR，清楚描述动机与改动范围；大改动建议先开 Issue 讨论 / Open a PR with a clear description; for large changes, open an issue first.

## 报告问题 / Reporting Issues

- Bug 报告请附：.NET 版本、操作系统、复现步骤、期望与实际行为 / Include .NET version, OS, repro steps, expected vs. actual behavior.
- **安全漏洞请勿公开提交**，请阅读 [SECURITY.md](SECURITY.md) / **Never report security vulnerabilities publicly** — see [SECURITY.md](SECURITY.md).

## 行为准则 / Code of Conduct

参与本项目即表示你同意遵守 [行为准则](CODE_OF_CONDUCT.md) / By participating, you agree to abide by the [Code of Conduct](CODE_OF_CONDUCT.md).

## 自动检查 / Automated checks

请在提交前参考 [CI 说明](docs/ci.md) 运行适用的构建与快速测试；集成和压力测试需要单独准备环境。

See [CI and dependency updates](docs/ci.md) for the checks to run before submitting a change.
