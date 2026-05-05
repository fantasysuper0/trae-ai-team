# 项目规范 — AI 开发团队共享

> 本文件是所有 Agent 的行为基础规范，会话开始时自动注入上下文。
> 修改此文件后请开启新对话以确保生效。

## 技术栈

- **前端**：React 18 + TypeScript + Tailwind CSS + Zustand
- **后端**：Node.js + Express + Prisma + PostgreSQL
- **测试**：Vitest（单元/集成） + Playwright（E2E）
- **CI/CD**：GitHub Actions
- **包管理**：pnpm

## 通用编码规范

- 变量命名使用小驼峰（camelCase）
- 组件/类/类型使用大驼峰（PascalCase）
- 常量使用全大写下划线（UPPER_SNAKE_CASE）
- 注释使用中文，占比不低于 15%
- 遵循 ESLint 规范，提交前必须通过 lint
- 优先使用开源框架和库，避免造轮子

## 目录结构约定

```
src/
├── components/       # 公共 UI 组件
├── views/            # 页面组件
├── api/              # 前端 API 请求层（基于 api-contract.yaml 生成）
├── services/         # 后端业务逻辑
├── models/           # 数据模型（Prisma schema）
├── routes/           # 后端路由定义
├── middleware/       # 中间件（认证、日志、错误处理）
├── utils/            # 工具函数
└── types/            # TypeScript 类型定义

tests/
├── unit/             # 单元测试
├── integration/      # 集成测试
└── e2e/              # 端到端测试

docs/
├── architecture.md   # 架构设计文档
├── api-contract.yaml # API 契约（OpenAPI 3.0）
└── tech-stack.md     # 技术选型文档
```

## 工作流规则

1. **契约先行**：API 接口变更必须先更新 `docs/api-contract.yaml`，再修改代码
2. **文件互斥**：禁止直接修改其他 Agent 正在编辑的文件，有冲突时通知 SOLO Coder 裁决
3. **提交前检查**：提交前必须运行 `pnpm lint && pnpm test`
4. **日志规范**：禁止使用 `console.log`，统一使用 `src/utils/logger` 模块
5. **错误处理**：所有 async 函数必须 try-catch，错误统一走 `src/utils/errorHandler`

## 文档约定

- 架构设计文档放在 `docs/architecture.md`
- API 契约放在 `docs/api-contract.yaml`（OpenAPI 3.0 格式）
- 技术选型文档放在 `docs/tech-stack.md`
- 每个 Agent 完成任务后必须更新对应文档

## Agent 角色定义

| 角色 | 职责 | 输出目录 |
|------|------|----------|
| Architect（架构师） | 系统设计、技术选型、API 契约 | `docs/` |
| Frontend（前端） | UI 组件、页面、API 对接 | `src/components/`, `src/views/`, `src/api/` |
| Backend（后端） | API 实现、业务逻辑、数据库 | `src/services/`, `src/routes/`, `src/models/` |
| QA（测试） | 集成测试、E2E 测试、契约验证 | `tests/` |
| DevOps（运维） | CI/CD 流水线、构建部署 | `.github/workflows/` |
| SOLO Coder（编排） | 任务分解、子 Agent 调度、代码审查 | 全局 |
