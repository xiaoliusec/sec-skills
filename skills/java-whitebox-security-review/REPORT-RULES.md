# Report Rules

本文件定义 Java 白盒安全审计 skill 的统一输出规范。

## 总体要求

1. 所有结论必须可复核
2. 所有高风险问题必须给出证据链
3. 不确定结论必须降级，不得强行确认
4. 报告重点是风险、证据、影响和修复建议
5. 不输出利用代码、payload 或攻击步骤

## 报告文件

建议输出以下文件：

- `summary.md`
- `routes.md`
- `auth-model.md`
- `findings.md`
- `config-review.md`
- `dependency-review.md`

## findings.md 结构

每个发现项使用如下格式：

```md
## [F-001] 标题

- Severity: High
- Confidence: confirmed
- Category: auth
- File: `src/main/java/...`
- Function: `com.example.UserController#deleteUser`
- Entry Point: `DELETE /api/users/{id}`
- Source: `@PathVariable id`
- Sink: `userService.deleteById(id)`

### Evidence
- 说明调用链
- 说明缺失的安全控制
- 引用关键代码片段

### Impact
- 说明影响的数据、能力或边界

### Recommendation
- 给出最小且可执行的修复建议

### Review Notes
- 标注需人工复核的点
```

## 证据要求

### confirmed

必须满足：

- 真实文件路径
- 明确的方法或路由
- 可解释的调用链或控制缺失点
- 安全控制缺失或失效的具体证据

### probable

适用于：

- 风险高度可疑
- 主要链路存在，但缺少局部验证
- 需要人工补充上下文确认

### suspicious

适用于：

- 仅有模式匹配命中
- 仅有部分调用链
- 控制逻辑复杂，暂无法确认

## 严重度建议

- `Critical`
  - 可直接导致敏感数据大规模泄露、远程命令执行或系统控制权风险
- `High`
  - 可导致未授权敏感操作、核心数据访问、关键边界突破
- `Medium`
  - 风险明确但需要额外条件，或影响范围相对有限
- `Low`
  - 配置缺陷、弱控制、低影响信息泄露

## summary.md 要求

必须包含：

- 项目概览
- 技术栈
- 审计范围
- 高风险摘要
- 发现项统计
- 优先修复建议

## routes.md 要求

至少记录：

- 路由
- 控制器
- 方法
- 参数来源
- 鉴权方式
- 风险备注

## auth-model.md 要求

至少记录：

- 认证入口
- 会话或 token 机制
- 角色/权限模型
- 资源归属校验点
- 管理接口保护方式
- 多租户边界控制
