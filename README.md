# SmartSearch MCP Server

An MCP server integrating the Cloudsway Smart Search API, providing web search functionality for MCP clients.

## Features

- Web search with pagination, language, freshness and site filtering
- Structured JSON output suitable for downstream processing
- MCP-compatible server configuration and deployment

## Tool: SmartSearch

Performs web search and returns structured results.

Input parameters:
- `query` (string, required): Search keywords (cannot be empty)
- `count` (int, optional): Number of results to return. Default: 10. Accepted values: 10, 20, 30, 40, 50. Max: 50.
- `offset` (int, optional): Zero-based offset for pagination. Default: 0.
- `setLang` (string, optional): Language code for results (recommended 4-letter codes like `en-US`). Default: `en`.
- `freshness` (string, optional): Time filter: `Day`, `Week`, `Month`, or a date range like `2023-02-01..2023-05-30`.
- `sites` (string, optional): Restrict results to a host (e.g., `github.com`).

## Response Structure

Successful response (JSON):

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

Key fields:
- `queryContext.originalQuery`: the submitted query
- `webPages.value[]`: list of result items with `name`, `url`, `snippet`, `datePublished`, `dateLastCrawled`, `siteName`, `thumbnailUrl`, `score`

## Error Handling

Common HTTP status codes:
- `200` — success
- `429` — rate limit exceeded (QPS limit reached)

For higher QPS or account issues, contact Cloudsway support.

## Configuration

### Obtain API Key
1. Register and obtain Endpoint and AccessKey at: https://console.cloudsway.ai
2. Combine them as: `{Endpoint}-{AccessKey}`

### Environment Variable
Set the combined key in your deployment environment as:
```bash
export SERVER_KEY="endpoint-accesskey"
```

Use `SERVER_KEY` in MCP deployment configuration.

## Deployment

- Entry file: `src/smartsearch/smartsearch.py`
- Ensure `SERVER_KEY` environment variable is provided to the running process.

### Example MCP Service Configuration
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
