---
name: cicd-setup
description: 配置 GitHub Actions CI/CD 流水线
---

# CI/CD 配置技能

## 描述
根据项目技术栈和部署需求，配置 GitHub Actions CI/CD 流水线。

## 何时使用
- 项目初始化，需要搭建 CI/CD
- 新增部署环境（staging/production）
- 需要添加新的自动化流程（代码质量、安全扫描等）
- DevOps Agent 执行 CI/CD 相关任务

## 指令

### 第一步：读取项目配置
1. 读取 `docs/tech-stack.md` 获取技术栈信息
2. 读取 `package.json` 获取脚本命令
3. 检查现有 `.github/workflows/` 配置

### 第二步：设计流水线
设计以下 Workflow：

#### 1. CI 流水线（`.github/workflows/ci.yml`）
```yaml
name: CI
on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]

jobs:
  lint:
    # 代码风格检查
  test:
    # 运行测试
  build:
    # 构建产物
    needs: [lint, test]
```

#### 2. CD 流水线（`.github/workflows/cd.yml`）
```yaml
name: CD
on:
  push:
    branches: [main]

jobs:
  deploy-staging:
    # 部署到预发环境
  deploy-production:
    # 部署到生产环境（需手动审批）
    needs: [deploy-staging]
```

### 第三步：输出配置文件
将 Workflow 文件输出到 `.github/workflows/` 目录。

## 当前技术栈
!`cat docs/tech-stack.md 2>/dev/null || echo "技术栈文档尚未创建"`

## 当前 package.json scripts
!`cat package.json 2>/dev/null | grep -A 20 '"scripts"' || echo "package.json 尚未创建"`

## 注意事项
- 使用 GitHub Actions 官方 Action（actions/checkout@v4 等）
- 敏感信息使用 GitHub Secrets，不硬编码
- 构建缓存加速（pnpm store、node_modules）
- 生产部署需要手动审批（environment + approval）
- 所有 Workflow 必须包含失败通知
