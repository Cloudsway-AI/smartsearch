# 智能搜索 MCP 服务器

一个集成了远程智能搜索 API 的 MCP 服务器实现，提供强大的网页搜索功能。

## 特性

-   **网页搜索**：支持关键词检索，并可控制结果数量、分页、语言和安全等级。
-   **结构化 JSON 输出**：所有搜索结果均以清晰的 JSON 格式返回。
-   **轻松集成**：为与任何兼容 MCP 的客户端无缝使用而设计。

## 工具

### `smart_search`

执行网页搜索，支持过滤和分页选项。

**输入参数：**

-   `query` (string): 搜索关键词。
-   `count` (number, optional): 返回结果的数量 (默认: 10)。
-   `offset` (number, optional): 分页偏移量 (默认: 0)。
-   `setLang` (string, optional): 搜索语言 (例如, 'en', 'zh', 默认: 'en')。
-   `safeSearch` (string, optional): 安全等级 ('Strict', 'Moderate', 'Off', 默认: 'Strict')。

## 配置

### 获取 API 密钥

1.  注册一个搜索 API 提供商的账户。
2.  生成您的 API 密钥。密钥格式应为 `endpoint-apikey`。

### 环境变量

此服务器需要设置 `SERVER_KEY` 环境变量为您的 API 密钥。

## 在 MCP 客户端中使用

要将此服务器与 OpenWebUI 或 Claude Desktop 等客户端一起使用，请添加以下配置。此示例使用 `npx` 直接从 npm 注册表运行服务器。

**NPX 配置:**

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

此 MCP 服务器根据 MIT 许可证发布。更多详情请参阅 LICENSE 文件。
