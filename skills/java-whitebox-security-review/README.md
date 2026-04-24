# Java Whitebox Security Review

面向 Java Web 项目的防御性白盒安全审计 Skill。

## 设计目标

这个 skill 参考了成熟代码审计 skill 项目的共同做法：

- 主 `SKILL.md` 负责执行入口与控制逻辑
- `references/` 负责沉淀方法论、检查清单和框架专项规则
- `REPORT-RULES.md` 统一约束输出格式

这样比单个超长 `SKILL.md` 更易维护，也更方便后续拆出子 skill。

## 适用项目

- Spring Boot
- Spring MVC
- Spring Security
- Apache Shiro
- MyBatis
- JPA / Hibernate
- Servlet / JSP
- Java API 服务与后台系统

## 核心方法

### 1. 分阶段流水线

采用 `Phase 0 -> Phase 5` 的分阶段流程，先做项目侦察与入口梳理，再进入漏洞分析与证据校验。

### 2. 双轨审计模型

- `sink-driven`
  - 从危险汇点出发，逆向追踪 source、传播链和防护点
- `control-driven`
  - 从入口点出发，检查应存在但缺失的认证、授权、归属校验等控制

### 3. 证据驱动

所有发现项必须具备以下至少一组证据：

- 文件路径 + 方法名 + 调用链
- 路由位置 + 鉴权缺失点 + 敏感操作路径
- source -> sink 数据流关系

### 4. 反幻觉约束

不得基于惯例猜测项目结构；所有结论都应来自真实代码读取与验证。

## 目录说明

```text
java-whitebox-security-review/
├── SKILL.md
├── README.md
├── REPORT-RULES.md
└── references/
```

## 推荐扩展方向

后续可以继续拆为更细的子 skill：

- `java-route-mapper`
- `java-auth-audit`
- `java-sql-audit`
- `java-file-upload-audit`
- `java-audit-pipeline`

## 使用建议

- 小型项目用 `quick` 或 `normal`
- 涉及权限模型、后台管理、导入导出、文件处理时优先用 `deep`
- 审计完成后统一落报告到 `.monkeycode/security-review/java/`
