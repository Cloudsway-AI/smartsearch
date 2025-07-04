# Smart Search MCP Server

An MCP server implementation that integrates a remote smart search API, providing powerful web search capabilities.

## Features

-   **Web Search**: Perform web searches with controls for result count, pagination, language, and safety level.
-   **Structured JSON Output**: All search results are returned in a clean JSON format.
-   **Easy Integration**: Designed for seamless use with any MCP-compatible client.

## Tools

### `smart_search`

Executes a web search with filtering and pagination options.

**Inputs:**

-   `query` (string): The search terms.
-   `count` (number, optional): The number of results to return (default: 10).
-   `offset` (number, optional): The pagination offset (default: 0).
-   `setLang` (string, optional): The language for the search (e.g., 'en', 'zh', default: 'en').
-   `safeSearch` (string, optional): The safety level ('Strict', 'Moderate', 'Off', default: 'Strict').

## Configuration

### Getting an API Key

1.  Sign up for an account with the search API provider.
2.  Generate your API key. The key should be in the format `endpoint-apikey`.

### Environment Variable

This server requires the `SERVER_KEY` environment variable to be set to your API key.

## Usage with an MCP Client

To use this server with a client like OpenWebUI or Claude Desktop, add the following configuration. This example uses `npx` to run the server directly from the npm registry.

**NPX Configuration:**

```json
{
  "mcpServers": {
    "smart-search": {
      "command": "npx",
      "args": [
        "-y",
        "@zachtian/smartsearch"
      ],
      "env": {
        "SERVER_KEY": "YOUR_API_KEY_HERE"
      }
    }
  }
}
```

## License

This MCP server is released under the MIT License. See the LICENSE file for more details.
