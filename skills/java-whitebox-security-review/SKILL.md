---
name: java-whitebox-security-review
description: 面向 Java Web 项目的防御性白盒安全审计 Skill。基于分阶段流水线、双轨审计模型和证据驱动原则，对 Spring Boot、Spring MVC、Spring Security、Shiro、MyBatis、JPA、Hibernate、Servlet 等常见技术栈开展结构化源码安全审查，并输出可复核、可修复的审计报告。
arguments:
  - name: target
    description: 待审计项目路径，默认当前工作区
    required: false
  - name: scope
    description: 审计范围，可选 all、auth、dataflow、config、deps、report，默认 all
    required: false
  - name: depth
    description: 审计深度，可选 quick、normal、deep，默认 normal
    required: false
  - name: focus
    description: 重点关注项，多个用逗号分隔，例如 auth,sqli,upload,ssrf
    required: false
---

# Java 白盒安全审计

这是一个面向 Java Web 项目的防御性白盒安全审计 Skill。

目标不是泛化地“找关键字”，而是通过项目识别、入口梳理、双轨审计、证据校验和标准化报告，产出可信、可修复、可复核的审计结论。

本 Skill 仅用于合法的源码安全评审、SDL、安全内审和代码审查，不生成利用代码，不输出攻击 payload，不进行外部目标攻击验证。

## 目录结构

```text
java-whitebox-security-review/
├── SKILL.md
├── README.md
├── REPORT-RULES.md
└── references/
    ├── anti-hallucination.md
    ├── audit-phases.md
    ├── findings-template.md
    ├── java-sources-and-sinks.md
    ├── methodology.md
    ├── security-checklist.md
    ├── vulnerability-conditions.md
    └── java-frameworks/
        ├── mybatis.md
        ├── shiro.md
        ├── spring-mvc.md
        ├── spring-security.md
        └── servlet.md
```

## 执行原则

1. 先识别项目结构和技术栈，再下审计结论
2. 先梳理入口点和权限边界，再做漏洞分类分析
3. 同时使用双轨审计模型：
   - sink-driven：从危险汇点逆向追踪数据流
   - control-driven：从入口点正向检查缺失的安全控制
4. 所有发现项必须满足证据要求，不足时降级为可疑项
5. 报告中必须区分 confirmed、probable、suspicious
6. 不输出利用代码、PoC、绕过技巧或外部攻击步骤

## 执行流程

按 `references/audit-phases.md` 执行：

1. Phase 0：项目度量与规模判断
2. Phase 1：技术栈侦察与入口梳理
3. Phase 2：双轨安全审计
4. Phase 2.5：覆盖率与遗漏校验
5. Phase 3：证据一致性验证
6. Phase 4：规则沉淀（可选）
7. Phase 5：输出标准化报告

## 重点审计范围

按 `references/security-checklist.md` 检查以下问题：

- 认证与授权缺失
- 水平/垂直越权
- SQL 注入
- XSS
- SSRF
- 路径遍历
- 任意文件上传
- 反序列化风险
- 表达式注入
- 命令执行
- 不安全重定向
- 敏感信息泄露
- 硬编码密钥
- 错误配置
- 高风险依赖
- 业务敏感操作缺少二次校验

## 技术栈适配

优先识别并结合对应框架规则：

- Spring Boot / Spring MVC
- Spring Security
- Apache Shiro
- Servlet / Filter / Interceptor
- MyBatis
- JPA / Hibernate
- Jackson / Fastjson
- Thymeleaf / JSP / Freemarker

框架专项审计规则见：

- `references/java-frameworks/spring-security.md`
- `references/java-frameworks/shiro.md`
- `references/java-frameworks/mybatis.md`
- `references/java-frameworks/spring-mvc.md`
- `references/java-frameworks/servlet.md`

## 输出要求

最终输出必须符合 `REPORT-RULES.md` 和 `references/findings-template.md`。

至少应包含：

- 项目概览与技术栈
- 路由与入口点梳理
- 鉴权与资源边界建模
- 发现项清单
- 每个发现项的证据链
- 风险等级与置信度
- 修复建议
- 需人工复核项
- 审计结论摘要

## 建议生成的报告文件

建议输出到 `.monkeycode/security-review/java/`：

- `summary.md`
- `routes.md`
- `auth-model.md`
- `findings.md`
- `config-review.md`
- `dependency-review.md`

## 推荐搜索目标

优先查找以下文件与关键点：

- `pom.xml`
- `build.gradle`
- `application.yml`
- `application.properties`
- `SecurityConfig`
- `ShiroConfig`
- `@RestController`
- `@Controller`
- `@RequestMapping`
- `@PreAuthorize`
- `@Secured`
- `@RequiresPermissions`
- `MultipartFile`
- `RestTemplate`
- `WebClient`
- `ObjectInputStream`
- `Runtime.getRuntime().exec`
- `ProcessBuilder`
- `redirect:`
- `${`
- `@Select`
- `@Update`
- `@Delete`

## 成功标准

执行完成时，应满足：

- 说明清楚项目的安全边界与关键模块
- 列出主要外部入口与鉴权方式
- 高风险问题具备明确证据链
- 可疑点没有被误报为已确认漏洞
- 修复建议可直接交付开发团队
- 报告结构统一、可复查、可追踪

## Example Invocation

```text
/java-whitebox-security-review target=. scope=all depth=normal
```

```text
/java-whitebox-security-review target=./backend scope=auth depth=deep focus=auth,idor
```

```text
/java-whitebox-security-review target=. scope=config,deps depth=quick
```

## Final Response Style

完成后按如下顺序汇报：

1. 审计范围与识别到的技术栈
2. 关键发现项列表
3. 高风险问题的证据摘要
4. 需人工复核项
5. 已生成的报告文件
6. 优先修复建议
