# Servlet

重点检查：

- `doGet` / `doPost` 是否直接处理敏感操作
- Filter 链是否覆盖全部敏感路径
- 参数是否直接进入 SQL、文件系统或命令执行
- 下载与跳转逻辑是否存在路径或 URL 控制问题

高风险信号：

- 直接使用 `request.getParameter()` 构造危险操作
- 过滤器遗漏后台路径
