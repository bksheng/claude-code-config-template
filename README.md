## Claude Code Python 开发最佳实践配置

这是一个专为 Claude Code 打造的增强型配置模板集。通过安全沙箱、DeepSeek 模型适配以及自动备份回滚机制，为开发者提供一个高效、安全、可溯源的 AI 编程环境。

## 📂 文件说明

| 文件          | 用途                                     | 放置位置                |
| ------------- | ---------------------------------------- | ----------------------- |
| settings.json | 权限白名单/黑名单、模型路由、主题        | ~/.claude/settings.json |
| CLAUDE.md     | 项目级 AI 行为规范（备份/测试/代码风格） | ~/.claude/CLAUDE.md     |

## 🌟 核心特性

* 安全优先: 严格的黑名单机制，默认禁止 rm -rf /、系统重启及 .env 敏感文件读取。
* 自动备份: 修改前强制 .orig 备份，修改后记录 .v[n].bak 快照，支持版本回溯。
* 测试驱动: 强制集成 pytest，确保 AI 逻辑变更经过自动化测试验证。
* 中文优先: 针对中文开发者优化，交互提示与代码注释始终使用中文。
* 溯源清晰: 强制 Git 原子化提交，每一行 AI 代码都有据可查。

## 🚀 快速开始

      1. 安装 Claude Code: 按照官方指南安装 claude-code CLI。
      2. 部署配置: 复制本仓库的 settings.json 到 ~/.claude/settings.json。
      3. 设置密钥: 编辑 settings.json，将 ANTHROPIC_AUTH_TOKEN 替换为你的 DeepSeek 密钥。
      4. 项目集成: 将 CLAUDE.md 放置在 Python 项目根目录，Claude 会自动读取该准则。

## 🤖 模型路由 (DeepSeek 适配)

本配置已针对 DeepSeek API 进行优化，实现高性能与低成本的平衡：

| Claude 模型档位 | 映射模型 (DeepSeek) | 适用场景                     |
| --------------- | ------------------- | ---------------------------- |
| Opus            | deepseek-v4-pro[1m] | 复杂架构设计、大规模重构     |
| Sonnet          | deepseek-v4-flash   | 日常编码、快速修复、代码审查 |
| Haiku           | deepseek-v4-flash   | 简单的文件读取、搜索与询问   |

## 🛡️ 权限设计逻辑

* 默认模式: acceptEdits（自动接受编辑，提升效率）。
* 白名单思路: 开放“读、查、测、拷、移”。允许 AI 自主运行测试及管理依赖，但不赋予最高系统权限。
* 黑名单重点:
* 系统安全: 禁用 reboot, shutdown, mkfs, dd 等破坏性指令。
  * 隐私隔离: 严禁访问 ~/.ssh/, ~/.aws/, .env 及数据库二进制文件。
  * 自我保护: 禁止 AI 修改 settings.json 或 CI/CD 流程文件。

## ⚙️ 扩展与自定义

CLAUDE.md 采用模块化设计，你可以根据项目类型自由调整：

* Python 项目: 保留现有的 pip/pytest/ruff 规范。
* Node.js 项目: 将相关指令替换为 npm/vitest/eslint。
* 团队协作: 建议在 Git 提交规范中加入特定的前缀，如 feat(ai): [description]。

## 📄 开源协议

本项目基于 MIT 协议开源。
