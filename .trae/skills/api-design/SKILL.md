---
name: api-contract-gen
description: 根据架构设计生成或更新 OpenAPI 3.0 契约文档
---

# API 契约生成技能

## 描述
基于架构设计文档，生成标准化的 OpenAPI 3.0 契约文档，作为前后端开发的"合同"。

## 何时使用
- 架构设计完成后，需要生成 API 契约
- 新增 API 端点，需要更新契约
- API 接口变更，需要同步更新契约

## 指令

### 第一步：读取现有设计
1. 读取 `docs/architecture.md` 获取模块和接口定义
2. 读取现有 `docs/api-contract.yaml`（如果存在）

### 第二步：生成契约
对每个模块的每个 API 端点，定义以下内容：

```yaml
paths:
  /api/v1/{resource}:
    get:                    # HTTP 方法
      summary: 简要描述      # 中文描述
      tags: [模块名]         # 分组标签
      parameters:           # 请求参数
        - name: id
          in: path
          required: true
          schema:
            type: string
      responses:
        '200':
          description: 成功响应
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Resource'
        '400':
          $ref: '#/components/responses/BadRequest'
        '401':
          $ref: '#/components/responses/Unauthorized'
```

### 第三步：定义公共 Schema
在 `components/schemas/` 中定义所有数据模型：

```yaml
components:
  schemas:
    User:
      type: object
      required: [id, email, name]
      properties:
        id:
          type: string
          format: uuid
        email:
          type: string
          format: email
        name:
          type: string
        createdAt:
          type: string
          format: date-time
```

### 第四步：输出
将完整契约写入 `docs/api-contract.yaml`

## 当前契约内容
!`cat docs/api-contract.yaml 2>/dev/null || echo "契约文件尚未创建"`

## 当前架构文档
!`cat docs/architecture.md 2>/dev/null || echo "架构文档尚未创建"`

## 注意事项
- 契约是前后端的"合同"，必须精确无歧义
- 所有字段必须包含类型和描述
- 错误响应必须统一定义
- 版本号放在 URL 路径中（如 `/api/v1/`）
