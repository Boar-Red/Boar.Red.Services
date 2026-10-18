# 安全策略 / Security Policy

## 支持的版本 / Supported Versions

| 版本 / Version | 支持状态 / Supported |
| --- | --- |
| 10.x | ✅ 是 / Yes |
| < 10.0 | ❌ 否（请升级至 10.x）/ No (please upgrade to 10.x) |

## 报告漏洞 / Reporting a Vulnerability

请**不要**通过公开 Issue 报告安全漏洞。请使用 GitHub 的 [Security Advisories（安全公告）](../../security/advisories/new) 私下提交，或通过仓库维护者的其他私下渠道联系。

Please **do NOT** report security vulnerabilities through public issues. Use GitHub [Security Advisories](../../security/advisories/new) for a private report, or contact the maintainers through other private channels.

我们会在收到报告后尽快评估并回复。修复发布后，我们会在 CHANGELOG 中致谢（如你希望具名）。

We will assess and respond as soon as possible. After a fix is released, credit will be given in the CHANGELOG (named attribution upon request).

## 关于示例配置中的凭据 / About Credentials in Sample Configs

本框架各服务的 `ConfigFiles/` 配置文件中包含的管理员账号、服务密码与 AES 密钥**均为本地开发示例值**（如 `admin` / `123456` / 固定示例密钥），仅用于开箱运行演示。

The administrator accounts, service passwords and AES keys in the `ConfigFiles/` sample configs of each service are **local development examples only** (e.g. `admin` / `123456` / fixed sample keys), intended solely for out-of-the-box demos.

⚠️ **部署到任何非本地环境前，必须全部更换**；因未更换示例凭据而导致的安全问题不属于框架漏洞。

⚠️ **These MUST all be replaced before deploying anywhere beyond localhost.** Security issues caused by keeping the sample credentials are not considered framework vulnerabilities.
