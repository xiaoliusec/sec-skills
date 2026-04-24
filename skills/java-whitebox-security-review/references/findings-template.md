# Findings Template

每个发现项建议采用如下模板：

```md
## [F-001] 标题

- Severity: High
- Confidence: confirmed
- Category: sqli
- File: `src/main/java/...`
- Function: `com.example.OrderController#list`
- Entry Point: `GET /api/orders`
- Source: `@RequestParam sort`
- Sink: SQL 动态拼接

### Evidence
- 给出关键路径
- 给出关键代码证据
- 给出缺少的控制点

### Impact
- 说明影响面

### Recommendation
- 给出修复建议

### Review Notes
- 标记需复核内容
```
