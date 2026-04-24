# Spring Security

重点检查：

- `permitAll()` 是否放开敏感接口
- `anyRequest().authenticated()` 是否被更宽规则覆盖
- 方法级注解是否覆盖关键 service
- 自定义鉴权过滤器是否真正生效
- 角色判断后是否仍缺资源归属校验

高风险信号：

- 后台接口仅在前端隐藏
- 关键路由未进入安全链
- 只有登录校验，没有对象级授权
