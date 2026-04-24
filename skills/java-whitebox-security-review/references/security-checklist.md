# Security Checklist

## D1 注入

- SQL 注入
- HQL / JPQL 注入
- 命令执行
- 表达式注入
- 模板注入

## D2 认证

- 登录接口保护
- Token / Session 验证
- 认证过滤链完整性

## D3 授权

- 路由级权限控制
- 方法级权限控制
- 资源归属校验
- 多租户边界控制

## D4 反序列化

- Java 原生反序列化
- Jackson 默认类型
- Fastjson 风险配置

## D5 文件操作

- 文件上传
- 文件读取
- 文件下载
- 路径遍历

## D6 SSRF

- URL 抓取
- 回调测试
- 图片下载
- 外部资源代理

## D7 加密与密钥

- 硬编码密钥
- 弱摘要算法
- 不安全随机数

## D8 配置安全

- Actuator 暴露
- CORS 过宽
- Debug 开启
- Swagger 暴露

## D9 业务逻辑

- 越权
- Mass Assignment
- 审批流缺陷
- 状态机绕过

## D10 依赖与供应链

- 高风险依赖版本
- 已知 CVE 组件
- 非必要高危组件启用
