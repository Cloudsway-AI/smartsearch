# SmartSearch MCP Server

一个集成远程Cloudsway智能搜索 API 的 MCP 服务器，实现网页搜索功能。

## 特性

- **网页搜索**：支持关键词检索、分页、语言和安全等级选项
- **结构化返回**：所有结果以 JSON 格式返回
- **平台兼容**：适用于 ModelScope MCP 平台及兼容客户端

## 工具

### SmartSearch

- 执行网页搜索，支持分页与安全选项
- 输入参数：
  - `query` (string)：搜索关键词
  - `count` (number, optional)：返回结果数量（默认10）
  - `offset` (number, optional)：分页偏移（默认0）
  - `setLang` (string, optional)：搜索语言（默认'en'）
  - `safeSearch` (string, optional)：安全搜索等级（默认'Strict'）

## 配置

### 获取 API 密钥
1. 登录 [www.cloudsway.ai](www.cloudsway.ai) 或联系 info@cloudsway.ai 获取Endpoint 和 AccessKey
2. 按照 `{Endpoint}-{AccessKey}` 格式组成`SERVER_KEY`

### ModelScope 部署

- 在 ModelScope 部署本工具时，**在环境变量配置区填写你的 API 密钥（SERVER_KEY）**
- 入口文件：`src/smartsearch/smartsearch.py`

### 服务配置示例

```json
{
  "mcpServers": {
    "smartsearch": {
      "command": "npx",
      "args": [
        "-y",
        "@cloudsway-ai/smartsearch@0.1.0"
      ],
      "env": {
        "SERVER_KEY": "YOUR_API_KEY_HERE"
      }
    }
  }
}
```

## 许可证

本 MCP 服务器基于 MIT License 发布。你可以自由使用、修改和分发本软件，但需遵守 MIT License 条款。详情请参阅项目中的 LICENSE 文件。