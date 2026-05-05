---
name: test-generation
description: 为指定模块生成单元测试、集成测试或 E2E 测试
---

# 测试生成技能

## 描述
根据源代码和 API 契约，为指定模块生成对应级别的测试代码。

## 何时使用
- 新功能开发完成，需要编写测试
- 发现 Bug，需要补充回归测试
- 覆盖率不足，需要补充测试用例
- QA Agent 需要生成集成/E2E 测试

## 指令

### 第一步：分析目标
1. 识别需要测试的模块/文件
2. 分析模块的公共接口（导出的函数、类、API 端点）
3. 识别边界条件和异常场景

### 第二步：确定测试级别

| 级别 | 触发条件 | 放置目录 |
|------|----------|----------|
| 单元测试 | 测试单个函数/组件/工具 | `tests/unit/` |
| 集成测试 | 测试模块间交互/API 端点 | `tests/integration/` |
| E2E 测试 | 测试完整用户流程 | `tests/e2e/` |

### 第三步：编写测试
每个测试文件包含：

```typescript
import { describe, it, expect, vi, beforeEach, afterEach } from 'vitest';

describe('模块名称', () => {
  // 正常流程测试
  it('应该正确处理正常输入', () => {
    // Arrange
    const input = { ... };
    // Act
    const result = functionUnderTest(input);
    // Assert
    expect(result).toEqual({ ... });
  });

  // 边界条件测试
  it('应该正确处理空输入', () => { ... });

  // 异常场景测试
  it('应该在无效输入时抛出错误', () => { ... });
});
```

### 第四步：输出测试文件
- 测试文件命名：`{源文件名}.test.ts`
- 放置到对应目录
- 确保测试可通过 `pnpm test` 运行

## 当前 API 契约（用于集成测试）
!`cat docs/api-contract.yaml 2>/dev/null || echo "契约文件尚未创建"`

## 注意事项
- 使用中文 describe/it 描述
- Mock 外部依赖，不依赖真实服务
- 每个测试用例独立，不依赖执行顺序
- 测试数据使用工厂函数生成，避免硬编码
- 覆盖率目标：核心模块 > 80%
