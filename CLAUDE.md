# Claude Code 项目规范 (Project Guidelines)

## Project Context
- **开发环境**: Python
- **依赖管理**: 优先 `pip`，安装前检查 `requirements.txt`
- **代码标准**: PEP 8，注释与交互提示始终使用 **中文**

## Core Commands

### 1. 备份与版本管理
- **修改前**: 若不存在 `<file>.orig`，执行 `cp <file> <file>.orig`
- **修改后**: 检查序号，执行 `cp <file> <file>.v[n+1].bak`
- **Git 提交**: 逻辑完成后执行 `git commit -m "Claude: [简述改动]"`
- **状态告知**: 完成后告知用户：“初始备份已就绪 (<file>.orig) / 已保存版本快照 (<file>.v[n].bak)”

### 2. 验证与交付
- **自动测试**: 修改后必须执行 `pytest` 或相关测试
- **代码质量**: 优先使用 `ruff check --fix` 优化格式
- **结果报告**: 测试失败需分析日志并修复，或报告阻塞点

### 3. 回滚操作
- **彻底重置**: `cp <file>.orig <file>`
- **版本回溯**: 根据指定序号 `cp <file>.v[n].bak <file>`
- **清理**: 仅用户明确指令时执行 `rm *.orig *.bak`

## Permissions & Safety
- **静默操作**: `ls`, `cat`, `grep`, `read` 等只读操作直接执行
- **禁令**: 严禁删除 `/`, `~`, `.git`；禁止修改 `.env` 或敏感凭证

## Coding Style
- **函数式倾向**: 优先编写无副作用的纯函数
- **命名规范**: 变量 `snake_case`，类名 `PascalCase`
- **健壮性**: 必须包含类型注解 (`typing`) 和 `try-except` 捕获