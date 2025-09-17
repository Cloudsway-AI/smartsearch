# SmartSearch MCP 服务器

一个将 Cloudsway 智能搜索 API 集成到 MCP 的服务器，为 MCP 客户端提供网页搜索功能。

## 功能

- 支持分页、语言、时间范围和站点过滤的网页搜索
- 返回结构化 JSON，便于下游处理
- 兼容 MCP 的服务器配置与部署

## 工具：SmartSearch

执行网页搜索并返回结构化结果。

输入参数：
- `query` （string，必填）：搜索关键词（不能为空）
- `count` （int，可选）：返回的搜索结果数量。默认：10。可选值：10、20、30、40、50。最大：50。
- `offset` （int，可选）：用于分页的零起始偏移。默认：0。
- `setLang` （string，可选）：结果的语言代码（建议使用 4 字母代码，如 `en-US`）。默认：`en`。
- `freshness` （string，可选）：时间筛选：`Day`、`Week`、`Month`，或像 `2023-02-01..2023-05-30` 的时间范围。
- `sites` （string，可选）：限制返回指定站点的结果（例如 `github.com`）。

## 响应结构

成功响应（JSON）：

```json
{
  "queryContext": { "originalQuery": "your search query" },
  "webPages": {
    "value": [
      {
        "name": "Page Title",
        "url": "https://example.com/page",
        "displayUrl": "https://example.com/page",
        "snippet": "Description of the page content...",
        "datePublished": "2025-07-14T00:00:00.0000000",
        "dateLastCrawled": "2025-07-15T02:48:00.0000000Z",
        "siteName": "Example Website",
        "thumbnailUrl": "https://example.com/thumbnail.jpg",
        "score": 0.95
      }
    ]
  }
}
```

关键字段：
- `queryContext.originalQuery`：提交的查询词
- `webPages.value[]`：结果项列表，每项包含 `name`、`url`、`snippet`、`datePublished`、`dateLastCrawled`、`siteName`、`thumbnailUrl`、`score`

## 错误处理

常见 HTTP 状态码：
- `200` — 成功
- `429` — 请求 QPS 超限（速率限制）

如需更高 QPS 或账号相关问题，请联系 Cloudsway 支持。

## 配置

### 获取 API 密钥
1. 在 https://console.cloudsway.ai 注册并获取 Endpoint 与 AccessKey
2. 将两者组合为 `{Endpoint}-{AccessKey}`

### 环境变量
在部署环境中设置组合后的密钥：
```bash
export SERVER_KEY="endpoint-accesskey"
```

在 MCP 部署配置中使用 `SERVER_KEY`。

## 部署

- 入口文件：`src/smartsearch/smartsearch.py`
- 确保运行进程的环境变量中提供了 `SERVER_KEY`

### 示例 MCP 服务配置
```json
{
  "mcpServers": {
    "smartsearch": {
      "command": "npx",
      "args": [
        "-y",
        "@cloudsway-ai/smartsearch"
      ],
      "env": {
        "SERVER_KEY": "YOUR_API_KEY_HERE"
      }
    }
  }
}
```