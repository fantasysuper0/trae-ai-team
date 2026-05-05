---
alwaysApply: false
description: 当编写、修改或运行测试代码时使用此规则
---

# 测试策略

> 智能生效：AI 判断当前任务与测试相关时自动加载。

## 分层测试策略

### 单元测试（由开发 Agent 自行编写）
- **覆盖范围**：核心业务逻辑、工具函数、数据转换
- **放置目录**：`tests/unit/`
- **命名规则**：`*.test.ts`
- **要求**：每个新功能/修复必须包含对应单元测试

### 集成测试（由 QA Agent 编写）
- **覆盖范围**：模块间交互、API 端点、数据库操作
- **放置目录**：`tests/integration/`
- **命名规则**：`*.integration.test.ts`
- **要求**：覆盖关键业务流程

### E2E 测试（由 QA Agent 编写）
- **覆盖范围**：完整用户流程
- **放置目录**：`tests/e2e/`
- **命名规则**：`*.e2e.test.ts`
- **工具**：Playwright

## 测试编写规范

- 使用 `describe` / `it` 组织测试，描述使用中文
- 每个测试用例遵循 AAA 模式（Arrange-Act-Assert）
- Mock 外部依赖（API、数据库、文件系统）
- 测试文件与源文件目录结构保持一致
- 覆盖率目标：核心模块 > 80%

## 测试命令

```bash
# 运行所有单元测试
pnpm test

# 运行集成测试
pnpm test:integration

# 运行 E2E 测试
pnpm test:e2e

# 查看覆盖率
pnpm test:coverage
```
