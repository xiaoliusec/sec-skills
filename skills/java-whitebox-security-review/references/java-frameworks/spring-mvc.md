# Spring MVC

重点检查：

- Controller 路由是否显式受保护
- 参数校验是否只依赖前端
- 数据绑定是否存在 mass assignment 风险
- 文件上传下载接口是否集中处理

高风险信号：

- 关键接口缺少鉴权注解
- `@ModelAttribute` 直接绑定敏感字段
