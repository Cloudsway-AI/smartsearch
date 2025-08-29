# SmartSearch MCP Server

An MCP server integrating the remote Cloudsway Smart Search API, providing web search functionality.

## Features

- **Web Search**: Supports keyword search, pagination, language, and safety level options
- **Structured Output**: All results are returned in JSON format
- **Platform Compatibility**: Suitable for MCP platform and compatible clients

## Tools

### SmartSearch

- Performs web search with support for pagination and safety options
- Input parameters:
  - `query` (string): Search keywords
  - `count` (number, optional): Number of results to return (default: 10)
  - `offset` (number, optional): Pagination offset (default: 0)
  - `setLang` (string, optional): Search language (default: 'en')
  - `safeSearch` (string, optional): Safety search level (default: 'Strict')

## Configuration

### Obtain API Key
1. Log in to [www.cloudsway.ai](https://www.cloudsway.ai) or contact info@cloudsway.ai to get your Endpoint and AccessKey.
2. Combine them in the format `{Endpoint}-{AccessKey}` to form your `SERVER_KEY`.

### Deployment

- When deploying this tool, **enter your API key (`SERVER_KEY`) in the environment variable configuration area**.
- Entry file: `src/smartsearch/smartsearch.py`

### Example Service Configuration

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
