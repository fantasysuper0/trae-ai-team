---
alwaysApply: false
globs: "src/components/**,src/views/**,src/api/**,src/hooks/**,src/stores/**"
---

# 前端开发规则

> 指定文件生效：仅在编辑前端相关文件时自动加载。

## 组件规范

- 使用函数式组件 + Hooks，禁止使用 Class 组件
- Props 必须定义 TypeScript 接口，使用 `interface` 而非 `type`
- 组件文件命名使用 PascalCase，与组件名一致
- 每个组件文件只导出一个主组件

## 状态管理

- 全局状态使用 Zustand
- 组件局部状态使用 `useState` / `useReducer`
- 禁止 prop drilling 超过 2 层，超过时使用 Zustand 或 Context

## API 对接

- 必须基于 `docs/api-contract.yaml` 中的定义开发
- 不得自行假设接口格式或路径
- 请求/响应类型从契约定义中导入
- API 请求统一放在 `src/api/` 目录

## 样式规范

- 使用 Tailwind CSS 工具类
- 复杂样式提取为组件级 CSS Module
- 响应式设计：移动端优先（mobile-first）

## 性能要求

- 列表渲染必须使用 `key`
- 大列表使用虚拟滚动
- 图片使用懒加载
- 避免在渲染函数中创建新对象/函数
