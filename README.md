# Himalayas Remote Jobs MCP Server

Access thousands of remote job listings and company information directly from your AI coding assistant! This public MCP server provides real-time access to Himalayas.app's remote job database.

🌐 **Public Server URL:** `https://mcp.himalayas.app/sse`

## Available Tools

### 🔍 Job Search Tools

#### `search_jobs`
Search for specific jobs using keywords with advanced filtering.

**Parameters:**
- `keyword` (string, optional): Search term (e.g., 'Python', 'React', 'Product Manager', 'Data Scientist')
- `page` (number, optional): Page number for pagination (default: 1)
- `country` (string, optional): Filter jobs by country
- `worldwide` (boolean, optional): Show ONLY 100% remote jobs available worldwide

**Example usage:**
- "Search for Python developer jobs"
- "Find React jobs in the United States"
- "Look for product manager positions worldwide"

#### `get_jobs`
Retrieve the latest remote job listings with optional filtering.

**Parameters:**
- `page` (number, optional): Page number for pagination (default: 1)
- `country` (string, optional): Filter jobs by country (e.g., 'Canada', 'United States', 'UK', 'Germany')
- `worldwide` (boolean, optional): Show ONLY 100% remote jobs available worldwide (default: false)

**Example usage:**
- "Get remote jobs in Canada"
- "Show me worldwide remote opportunities"
- "Find jobs on page 2"

### 🏢 Company Search Tools

#### `search_companies`
Search for specific companies using keywords.

**Parameters:**
- `keyword` (string, optional): Search term (e.g., 'startup', 'fintech', 'AI', company name)
- `page` (number, optional): Page number for pagination (default: 1)
- `country` (string, optional): Filter companies by country
- `worldwide` (boolean, optional): Show only companies with 100% remote jobs available worldwide

**Example usage:**
- "Search for AI startups"
- "Find fintech companies with remote jobs"
- "Look for companies named 'Stripe'"

#### `get_companies`
Browse remote-friendly companies with optional filtering.

**Parameters:**
- `page` (number, optional): Page number for pagination (default: 1)
- `country` (string, optional): Filter companies by country
- `worldwide` (boolean, optional): Show only companies with 100% remote jobs available worldwide

**Example usage:**
- "Show me remote companies in Europe"
- "Find companies with worldwide remote jobs"

## Setup Instructions

### 🖥️ Claude Desktop

1. Open Claude Desktop and navigate to **Settings → Developer → Edit Config**
2. Replace the content with this configuration:

```json
{
  "mcpServers": {
    "himalayas": {
      "command": "npx",
      "args": ["mcp-remote", "https://mcp.himalayas.app/sse"]
    }
  }
}
```

3. Save the file and restart Claude Desktop (Cmd/Ctrl + R)
4. When Claude restarts, a browser window will open for OAuth login - complete the authorization
5. You'll see the Himalayas tools available by clicking the tools icon (🔨) in the bottom right

### ⚡ Cursor

1. Open Cursor and go to **Settings → Features → Rules for AI**
2. Choose **Type: "Command"**
3. In the **Command** field, enter:
```bash
npx mcp-remote https://mcp.himalayas.app/sse
```
4. Save the configuration and restart Cursor
5. Complete the OAuth flow when prompted

### 🌊 Windsurf

1. Edit your `mcp_config.json` file
2. Add this configuration:

```json
{
  "mcpServers": {
    "himalayas": {
      "command": "npx",
      "args": ["mcp-remote", "https://mcp.himalayas.app/sse"]
    }
  }
}
```

3. Save the file and restart Windsurf
4. Complete the OAuth authorization when prompted

## Example Conversations

Once connected, you can have natural conversations with your AI assistant:

### Job Searching
- *"I'm looking for remote Python developer jobs in Europe"*
- *"Show me the latest remote data science positions"*
- *"Find part-time remote marketing jobs worldwide"*
- *"Search for senior software engineer roles in Canada"*

### Company Research
- *"Find AI startups that offer remote work"*
- *"Show me fintech companies with remote opportunities"*
- *"Look for companies in Germany that hire remotely"*
- *"Find verified companies with 4-day work weeks"*

### Advanced Queries
- *"Compare remote job opportunities between the US and UK"*
- *"Find companies that offer both remote work and competitive salaries"*
- *"Show me the tech stack used by remote-first companies"*

## What You'll Get

Each response includes rich, formatted information:

### Job Listings
- 🚀 Job title and company name
- 💼 Employment type (Full-time, Part-time, Contract)
- 🌍 Location restrictions or worldwide availability
- 💰 Salary ranges and currency
- 🛠️ Required skills and technologies
- 🔗 Direct application links
- 🏢 Company verification status

### Company Profiles
- 🏢 Company name and verification status
- 👥 Company size and founding year
- 🌍 Locations and remote work policies
- 🔥 Number of open positions
- 🎁 Benefits and perks information
- ⚡ Technology stacks used
- 🌐 Company website and social links

## Troubleshooting

### Connection Issues
- Ensure you have Node.js installed for the `npx` command
- Try restarting your AI assistant after configuration changes
- Clear authentication cache if needed: `rm -rf ~/.mcp-auth`

### Authentication Problems
- Complete the OAuth flow in the browser window that opens
- Make sure you're using the correct server URL: `https://mcp.himalayas.app/sse`
- Check that your internet connection is stable

### Tool Not Appearing
- Verify the configuration file syntax is correct (valid JSON)
- Restart your AI assistant completely
- Check the tools icon/menu in your AI assistant's interface

## Support

If you encounter any issues:
1. Check the troubleshooting section above
2. Verify your configuration matches the examples exactly
3. Try the connection with the [MCP Inspector](https://modelcontextprotocol.io/docs/tools/inspector) first

---

**Powered by [Himalayas.app](https://himalayas.app)** - The best place to find remote jobs and companies 🏔️
