# Installing the Himalayas MCP server

Himalayas is a remote MCP server. There is nothing to download, build or run locally: point the client at the hosted endpoint.

- Endpoint: `https://mcp.himalayas.app/mcp`
- Transport: Streamable HTTP (the old `/sse` endpoint is retired)
- API key: none

## Cline

Add this entry to `cline_mcp_settings.json` (in the VS Code extension: MCP Servers, Configure, Configure MCP Servers; in the Cline CLI: `~/.cline/mcp.json`):

```json
{
  "mcpServers": {
    "himalayas": {
      "type": "streamableHttp",
      "url": "https://mcp.himalayas.app/mcp",
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

Set `"type": "streamableHttp"` explicitly. Don't add an `Authorization` header.

## What works without signing in

Remote job search and job details, related jobs, companies, salary data and remote work statistics work as soon as the server is connected. A good first check is asking for "remote product manager jobs open to Canada".

## Account tools

The profile, application tracker, tailored resumes and cover letters, interview practice, messages, employer job posting and talent search tools use the user's Himalayas account through OAuth 2.1 with PKCE. A client that supports MCP OAuth opens a Himalayas sign-in page the first time one of these tools is called. A client that doesn't support MCP OAuth can still use the public tools above.

## Verify

After connecting, the server lists 79 tools. Calling `search_jobs` with `{"keyword": "product manager"}` returns current remote jobs.

Full setup for other clients: https://himalayas.app/docs/remote-jobs-mcp
