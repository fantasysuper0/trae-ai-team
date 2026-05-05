---
alwaysApply: true
---

# 编码规范补充

> 始终生效：所有 Agent 的所有对话都会加载此规则。

## 错误处理

- 所有 async 函数必须 try-catch
- 错误统一走 `src/utils/errorHandler`
- API 错误响应格式：

```typescript
{
  code: number;       // 业务错误码
  message: string;    // 错误描述（中文）
  details?: object;   // 可选的详细信息
}
```

- HTTP 状态码规范：
  - 200：成功
  - 201：创建成功
  - 400：请求参数错误
  - 401：未认证
  - 403：无权限
  - 404：资源不存在
  - 500：服务器内部错误

## Git 提交规范

- 格式：`type(scope): description`
- type 取值：`feat` | `fix` | `refactor` | `test` | `docs` | `ci` | `chore`
- 示例：
  - `feat(auth): add JWT token refresh`
  - `fix(api): handle null response from user service`
  - `test(user): add integration tests for login flow`

## 代码质量

- 单个函数不超过 50 行
- 单个文件不超过 300 行
- 嵌套层级不超过 3 层
- 避免不必要的对象复制或克隆
- 尽早 return，减少嵌套
