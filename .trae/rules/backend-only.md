---
alwaysApply: false
globs: "src/services/**,src/models/**,src/routes/**,src/middleware/**,prisma/**"
---

# 后端开发规则

> 指定文件生效：仅在编辑后端相关文件时自动加载。

## API 实现

- 必须严格匹配 `docs/api-contract.yaml` 的定义
- 不得擅自修改接口签名（路径、方法、参数、响应格式）
- 如需变更契约，必须先与 Architect Agent 确认并更新契约文件
- 路由定义放在 `src/routes/`，业务逻辑放在 `src/services/`

## 数据库

- 使用 Prisma ORM，禁止直接写 SQL
- 所有查询必须有适当的索引覆盖
- 数据库迁移文件命名格式：`YYYYMMDDHHMMSS_description`
- 迁移文件必须可回滚

## 安全规范

- 所有 API 端点必须经过认证中间件（公开接口除外）
- 输入验证使用 Zod schema
- 密码使用 bcrypt 哈希存储
- SQL 注入防护：Prisma 参数化查询
- XSS 防护：输出转义

## 日志规范

- 使用 `src/utils/logger` 模块
- 日志级别：`error` > `warn` > `info` > `debug`
- 生产环境日志级别不低于 `info`
- 敏感信息（密码、token）不得出现在日志中
