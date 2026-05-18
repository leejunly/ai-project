---
name: api-example-check
description: Use when checking API documentation pages for compliance with industry-standard REST API conventions. Covers URL design, HTTP methods, status codes, request/response formats, authentication, error handling, pagination, versioning, and example completeness.
version: 1.0.0
author: Hermes Agent
license: MIT
metadata:
  hermes:
    tags: [api, documentation, review, rest, quality, standards]
    related_skills: [requesting-code-review, writing-plans]
---

# API Example Check — API 文档规范性检查

## Overview

根据 REST API 业界主流规范（RFC 7231 / OpenAPI 3.x / JSON:API / Google API Design Guide / Microsoft REST API Guidelines），对 API 文档页面进行**结构化审查**，输出分级问题清单。

触发：用户提供 API 文档 URL 或文档内容，要求检查规范性。

## When to Use

- 用户给出 API 文档链接，要求审查文档质量
- 用户粘贴 API 文档片段，要求判断是否规范
- 用户说"帮我看看这个 API 文档写得好不好"
- 用户说"检查一下这个接口定义是否规范"

**不要用于：**
- 代码实现审查（用 `requesting-code-review`）
- API 功能测试 / 可用性测试
- 非 REST 风格（GraphQL、gRPC、WebSocket）的文档审查

## 检查流程

### 第一步：获取文档内容

1. 如果用户给的是 URL，用 `browser_navigate` + `browser_snapshot` 获取全文
2. 如果页面有反爬保护（CAPTCHA），需先启动 Camofox：`cd ~/tools/camofox-browser && npm start`（后台运行在 localhost:9377）
3. 如果 snapshot 截断或 scroll 超时，用 `browser_console` 执行 JS 提取 innerText（详见 `references/content-extraction.md`）
4. 如果用户粘贴的是文档文本，直接使用
5. 如果文档是飞书文档，使用 `feishu_doc_read` 读取

### 第二步：逐项检查

按以下维度逐项审查，每项标记为 ✅ 通过 / ⚠️ 建议改进 / ❌ 不符合规范：

---

## 检查清单

### 1. URL 设计（RESTful 命名）

| 检查项 | 规范要求 |
|--------|----------|
| 资源名用复数名词 | `/users` 而非 `/user`、`/getUsers` |
| 层级关系用路径表达 | `/users/{id}/orders` |
| 不用动词 | 避免 `/getUser`、`/createOrder`，用 HTTP 方法表达动作 |
| 使用短横线分隔 | `/user-orders` 而非 `/user_orders` 或 `/userOrders` |
| 全部小写 | `/users` 而非 `/Users` 或 `/USERS` |
| 避免文件扩展名 | 不用 `.json`、`.xml`、`.php` 后缀 |
| 避免深层嵌套 | 建议不超过 3 层（`/a/{id}/b/{id}/c` 为上限） |

### 2. HTTP 方法使用

| 方法 | 正确用途 | 常见误用 |
|------|----------|----------|
| `GET` | 获取资源（幂等、安全） | 用于修改数据、URL 过长时用 body 传参 |
| `POST` | 创建资源 | 用于幂等更新（应用 PUT） |
| `PUT` | 全量更新（幂等） | 用于部分更新（应用 PATCH） |
| `PATCH` | 部分更新 | 文档未说明只传变更字段 |
| `DELETE` | 删除资源（幂等） | 返回 200 + 空 body 而非 204 |

### 3. 请求参数

| 检查项 | 规范要求 |
|--------|----------|
| 路径参数 | 在 URL 中使用 `{paramName}` 标注 |
| 查询参数 | 命名用 camelCase 或 snake_case 并全文统一 |
| 分页参数 | 应有 `page`/`offset` + `limit`/`pageSize` |
| 排序参数 | 建议 `sort` + `order`（asc/desc）|
| 筛选参数 | 建议 `filter` 或直接使用字段名 |
| 字段选择 | 建议支持 `fields` 参数做稀疏字段集 |
| 参数类型 | 每个参数需注明类型（string / int / boolean / array） |
| 必填/可选 | 每个参数需标注 required 或 optional |
| 默认值 | 可选参数有默认值的应注明 |
| 取值范围/枚举 | 有限值集合的参数应列出所有可选值 |

### 4. 请求体（Request Body）

| 检查项 | 规范要求 |
|--------|----------|
| Content-Type | 需明确标注（通常 `application/json`） |
| 字段结构 | 嵌套对象/数组需展开说明 |
| 字段类型 | 每个字段需注明数据类型 |
| 必填字段 | 标注哪些字段必传 |
| 字段约束 | 注明最大/最小长度、正则格式、取值范围 |
| 示例 | 提供完整的 JSON 请求体示例 |
| 示例可复制 | 示例 JSON 应格式正确、可直接复制使用 |

### 5. 响应格式

| 检查项 | 规范要求 |
|--------|----------|
| 响应结构 | 顶层结构统一（如统一的 `code`/`message`/`data` 包装） |
| 字段说明 | 响应体每个字段需有说明 |
| 成功示例 | 每种状态码应提供对应的响应示例 |
| 分页响应 | 应返回 `total`/`page`/`pageSize` 等元信息 |

### 6. HTTP 状态码

| 状态码 | 正确使用场景 | 常见误用 |
|--------|------------|----------|
| `200 OK` | GET/PUT/PATCH 成功 | POST 创建成功返回 200 而非 201 |
| `201 Created` | POST 创建成功 | 未返回 Location 头指向新资源 |
| `204 No Content` | DELETE 成功、无返回内容 | 返回 200 + 空 body |
| `400 Bad Request` | 参数校验失败 | 返回信息不明确（应告知哪个字段错误） |
| `401 Unauthorized` | 未认证 / token 无效 | 和 403 混淆（401=未登录，403=无权限） |
| `403 Forbidden` | 已认证但无权访问 | 误用于未认证场景 |
| `404 Not Found` | 资源不存在 | 路径错误也返回 404 应区分 |
| `409 Conflict` | 资源冲突（如重复创建） | 用 400 代替 |
| `422 Unprocessable Entity` | 语义错误（参数合法但业务不通过） | 用 400 代替 |
| `429 Too Many Requests` | 频率限制 | 未返回 Retry-After 头 |
| `500 Internal Server Error` | 服务端异常 | 把业务错误也返回 500 |

### 7. 错误响应

| 检查项 | 规范要求 |
|--------|----------|
| 错误格式统一 | 所有错误应有统一结构（error_code / message / details） |
| 错误码体系 | 应有可追溯的业务错误码，非仅 HTTP 状态码 |
| 详细信息 | 错误信息应具备可操作性（告知用户如何修正） |
| 示例 | 至少提供一种错误响应示例 |
| 不泄露敏感信息 | 不应返回堆栈跟踪或内部实现细节 |

### 8. 认证与鉴权

| 检查项 | 规范要求 |
|--------|----------|
| 认证方式 | 明确说明（Bearer Token / API Key / OAuth 2.0） |
| Token 传递位置 | 说明在 Header（推荐）还是 Query 参数 |
| Header 名称 | 规范为 `Authorization: Bearer <token>` |
| Token 获取方式 | 应说明如何获取 token/API key |
| 权限范围 | 应说明 token 的权限粒度（scope） |

### 9. 版本管理

| 检查项 | 规范要求 |
|--------|----------|
| 版本策略 | 说明版本号规则（语义化版本） |
| 版本传递 | 说明是 URL 路径（`/v1/`）还是 Header（`Accept-Version`） |
| 废弃策略 | 说明旧版本何时下线、如何迁移 |

### 10. 示例完整性

| 检查项 | 规范要求 |
|--------|----------|
| 请求示例 | 每个接口至少一个完整请求示例（含 URL + Headers + Body） |
| 响应示例 | 每个状态码至少一个响应示例 |
| curl 示例 | 建议提供可直接执行的 curl 命令 |
| 多语言示例 | 可选但加分（Python / JS / Java 等） |

### 11. 补充检查

| 检查项 | 规范要求 |
|--------|----------|
| 接口概述 | 每个接口应有简介说明其用途 |
| 速率限制 | 应说明频率限制规则 |
| 幂等性说明 | POST 是否支持幂等 Key 应注明 |
| 日期时间格式 | 统一用 ISO 8601（`2024-01-01T00:00:00Z`） |
| 布尔值格式 | 统一 `true/false`，不用 `1/0` 或 `"yes"/"no"` |
| 空值表示 | 统一用 `null`，不用 `""` 或 `"null"` |

---

## 输出格式

审查结果按以下结构输出：

```
## 📋 API 文档审查报告

**文档来源**：<URL 或来源说明>
**审查时间**：<当前时间>
**接口数量**：<N 个>
**总体评分**：<优秀/良好/需改进/不合格>

---

### 🔴 严重问题（必须修复）

| # | 接口 | 问题 | 建议 |
|---|------|------|------|

### 🟡 建议改进

| # | 接口 | 问题 | 建议 |
|---|------|------|------|

### 🟢 做得好的地方

- ...

---

### 📊 各维度得分

| 维度 | 状态 |
|------|------|
| URL 设计 | ✅/⚠️/❌ |
| HTTP 方法 | ✅/⚠️/❌ |
| 请求参数 | ✅/⚠️/❌ |
| 请求体 | ✅/⚠️/❌ |
| 响应格式 | ✅/⚠️/❌ |
| 状态码 | ✅/⚠️/❌ |
| 错误响应 | ✅/⚠️/❌ |
| 认证鉴权 | ✅/⚠️/❌ |
| 版本管理 | ✅/⚠️/❌ |
| 示例完整性 | ✅/⚠️/❌ |
```

---

## 审查原则

1. **务实优先**：不是所有规范都适用，优先检查影响开发效率的问题（如缺少示例、参数类型不明确）
2. **分级处理**：区分"不能用的"（🔴）和"可以更好的"（🟡）
3. **给出具体建议**：不只说"不符合规范"，要给出正确写法
4. **引用标准**：具体问题引用对应的 RFC 编号或行业规范名称
5. **不强行套用**：内部 API、小团队 API 可以适当降低标准；对外公开 API 应严格要求

## Common Pitfalls

1. **只看表面**：检查 URL 命名后，也要检查实际返回的状态码是否合理
2. **忽略错误场景**：多数文档只写成功案例，错误处理才是排除故障的关键
3. **双重标准**：全文应统一命名风格（不要有的用 snake_case 有的用 camelCase）
4. **审查 ≠ 测试**：文档规范检查不验证 API 是否能通，那是功能测试的活
5. **不要只看一个接口**：需要检查所有接口之间的风格一致性

## Verification Checklist

- [ ] 已获取完整文档内容（非截断）
- [ ] 已覆盖所有检查维度
- [ ] 每个问题都给出了具体建议
- [ ] 区分了严重问题和改进建议
- [ ] 输出了得分表格
- [ ] 问题都附带了接口名称/路径方便定位
