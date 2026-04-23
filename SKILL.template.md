---
name: your-skill-name
description: 一句话描述这个 skill 的用途、适用场景和边界
---

# Goal

说明这个 skill 要解决什么问题。

示例：
- 自动分析本地项目中的接口定义
- 生成测试清单或文档
- 辅助执行某类重复性开发任务

# When To Use

说明什么时候应该使用这个 skill。

示例：
- 用户明确要求执行某类标准化任务
- 项目中存在固定目录、固定文件格式、固定工作流
- 需要输出统一结构的文档、代码或报告

# When Not To Use

说明什么时候不应该使用。

示例：
- 用户只是提问，不需要改代码
- 缺少必要输入文件
- 任务超出 skill 的职责范围
- 需要外部授权或敏感访问能力

# Inputs

列出这个 skill 需要的输入。

示例：
- 目标目录：`src/modules/user`
- 接口文档：`openapi.yaml`
- 测试框架：`pytest` / `jest`
- 输出目录：`.monkeycode/output/...`

# Outputs

列出这个 skill 的输出产物。

示例：
- 汇总文档
- 任务清单
- 测试用例草稿
- 代码骨架
- 报告文件

# Constraints

写清楚边界和限制。

示例：
- 仅处理工作区内文件
- 不读取敏感凭据文件
- 不执行高风险网络操作
- 不修改无关文件
- 优先做最小必要改动

# Workflow

按步骤描述执行流程。

1. 校验输入是否存在
2. 读取相关文件和目录结构
3. 提取关键信息
4. 生成中间结果
5. 生成最终输出
6. 如有需要，运行验证命令

# File Discovery

说明优先查找哪些文件。

示例：
- `package.json`
- `openapi.yaml`
- `src/**/*`
- `.monkeycode/docs/**/*`

# Implementation Notes

补充实现细节和约定。

示例：
- 优先复用现有目录结构
- 遵循项目已有命名风格
- 新增文件尽量少
- 文档输出保持固定标题结构

# Verification

说明如何验证结果。

示例：
- 检查输出文件是否生成
- 检查 Markdown 结构是否完整
- 运行相关测试或 lint
- 人工抽样核对关键字段

# Response Style

说明执行完成后如何向用户汇报。

示例：
- 先给结果摘要
- 再列出改动文件
- 最后说明验证结果和未完成项

# Example Invocation

给几个调用示例。

示例：
- `/your-skill-name path=src/modules/user`
- `/your-skill-name spec=openapi.yaml framework=pytest`
- `/your-skill-name output=.monkeycode/generated`

# Execution Template

执行时可遵循以下提示词骨架：

- 目标：<填写本次任务目标>
- 输入：<填写路径/文件/参数>
- 约束：<填写不可越界的限制>
- 输出：<填写要生成的文件或结果>
- 验证：<填写验证命令或检查方式>

请先检查输入是否存在，再按 Workflow 执行，并在结束时输出：
1. 完成了什么
2. 生成/修改了哪些文件
3. 如何验证
4. 还缺什么信息
