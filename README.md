# Himalayas Remote Jobs MCP Server

Search remote jobs, post job listings, find remote candidates, check salary benchmarks, and manage your career — all through AI conversation. The Himalayas MCP server connects your AI assistant to the [Himalayas](https://himalayas.app) remote jobs marketplace in real time.

Works with any AI platform that supports MCP servers, including **Claude** (Desktop, Code, Cowork), **ChatGPT**, **Gemini**, **Cursor**, **Windsurf**, **VS Code**, **Openclaw**, and **Microsoft Copilot Studio**.

**Server URL (Streamable HTTP — recommended):** `https://mcp.himalayas.app/mcp`
**Server URL (SSE — legacy fallback):** `https://mcp.himalayas.app/sse`

## Search for remote jobs with AI

Ask your AI assistant to find remote jobs and it searches the Himalayas marketplace in real time — over 100,000 listings with filters for salary, country, experience level, employment type, skills, and more.

- "Find remote Python developer jobs paying over $150K"
- "Show me senior React positions in Canada"
- "Search for part-time contractor roles worldwide"
- "What remote data science jobs were posted this week?"
- "Find entry-level marketing roles that offer health insurance"

Each result includes the full job description, salary range, company details, screening questions, and a direct application link. Use `get_related_jobs` to find similar roles, or `get_job_details` for the complete posting.

## Check remote salary data

Get salary benchmarks for any remote role by job title, seniority, and country. The data returns minimum, median, and maximum salaries in USD with fuzzy matching on job titles — you don't need to know the exact title.

- "What's the average salary for a Senior Product Manager?"
- "Compare salaries for React developers in the US vs Canada"
- "Show me salary benchmarks for DevOps engineers in Europe"
- "What do remote data engineers make at the senior level?"

## Post remote jobs with AI

Describe the role you're hiring for in natural language and the AI structures and submits the posting. Jobs are free to post on Himalayas. No form filling, no dashboard — just conversation.

- "Post a remote Senior Frontend Engineer role at $140-170K, full-time, worldwide"
- "Create a job listing for a Part-time Customer Support Specialist with screening questions"
- "Post a React developer role and add a question about TypeScript experience"
- "Show me how our job postings are performing"

Supports screening questions (boolean, text, multiple choice), salary ranges, skill tags, and optional paid extras for promoted placement (sticky $199, newsletter $99). You can also post without a Himalayas account using the `post_job_public` tool.

For the full employer workflow, see [How to Hire Remote Talent with AI](https://himalayas.app/docs/hire-with-ai).

## Find remote candidates and recruit with AI

Search 100K+ remote candidate profiles by keyword, country, and skills — completely free, no account or API key required. Every candidate on Himalayas has opted into remote work, so the signal is clean.

- "Find React developers in Canada who are open to new roles"
- "Search for senior engineers with Python and Kubernetes experience"
- "Show me product managers in Europe who are actively searching"
- "Find UX designers with fintech experience"

Each result includes the candidate's current role, company, skills, salary expectations, and career search status (actively searching, open to roles, or not looking). Visit their profile on Himalayas to message them directly — messaging is free and unlimited for all employers.

## Research remote companies

Get full company profiles including tech stack, benefits, open positions, employee count, and social links. Compare companies or research competitors before applying or hiring.

- "Tell me about Stripe's remote work setup"
- "Find companies that use React and offer unlimited PTO"
- "Which companies in Germany are hiring remotely?"
- "What benefits does GitLab offer?"

## Track job applications with AI

Save jobs to a kanban-style application tracker with statuses (saved, applied, interviewing, negotiation, hired, archived), excitement ratings, salary notes, and free-text notes. Manage your entire job search pipeline through conversation.

- "Save this job to my application tracker"
- "Move the Stripe application to interviewing stage"
- "Show me all the jobs I've applied to"
- "Update my notes on the Figma role — second interview scheduled for Friday"

## Manage your career profile with AI

Update your Himalayas profile, add work experience and education, and set your job search status — all through conversation. Your profile is visible to employers searching the talent directory.

- "Update my profile to actively searching"
- "Add my new role at Acme Corp as a Senior Engineer"
- "Set my tech stack to React, TypeScript, Node.js, and PostgreSQL"
- "Update my salary expectation to $160-180K"

---

## Setup

### Claude Desktop

1. Open your config file:
   - **macOS/Linux:** `~/Library/Application Support/Claude/claude_desktop_config.json`
   - **Windows:** `%APPDATA%\Claude\claude_desktop_config.json`

2. Add the Himalayas MCP server:

```json
{
  "mcpServers": {
    "himalayas": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://mcp.himalayas.app/mcp"]
    }
  }
}
```

3. Save and restart Claude Desktop.

### Claude Code

```bash
claude mcp add himalayas -- npx -y mcp-remote https://mcp.himalayas.app/mcp
```

### ChatGPT

MCP support in ChatGPT is rolling out progressively. Check your ChatGPT settings for MCP server configuration. Use the server URL `https://mcp.himalayas.app/mcp`.

### Gemini

MCP support in Gemini is rolling out progressively. Use the server URL `https://mcp.himalayas.app/mcp` when configuring MCP servers in your Gemini setup.

### Cursor

**One-click install:** Visit [himalayas.app/mcp](https://himalayas.app/mcp) and click the install button.

**Manual setup:** Open Cursor Settings → MCP → Add server with Type "Command":

```
npx mcp-remote https://mcp.himalayas.app/mcp
```

### Windsurf

Edit `~/.codeium/windsurf/mcp_config.json`:

```json
{
  "mcpServers": {
    "himalayas": {
      "command": "npx",
      "args": ["mcp-remote", "https://mcp.himalayas.app/mcp"]
    }
  }
}
```

Save and restart Windsurf.

### Microsoft Copilot Studio

Add the Himalayas MCP server URL `https://mcp.himalayas.app/mcp` in your Copilot Studio MCP configuration. See [Microsoft's MCP documentation](https://learn.microsoft.com/en-us/microsoft-copilot-studio/) for setup details.

### Openclaw

Add the Himalayas MCP server in your Openclaw MCP configuration using the server URL `https://mcp.himalayas.app/mcp`.

### VS Code, Zed, Cline, Continue, and others

The Himalayas MCP server works with any MCP-compatible client. Connect to `https://mcp.himalayas.app/mcp` (Streamable HTTP) or `https://mcp.himalayas.app/sse` (SSE fallback).

## Authentication

Public tools — job search, salary data, company research, talent search — work without any authentication or API key.

Authenticated tools use **OAuth 2.1 with PKCE**. When you first use a profile, tracker, or employer tool, your AI assistant opens a secure login page. Log in with your free Himalayas account, and your session persists with automatic token refresh.

## Tool Reference

<details>
<summary><strong>Public tools (no authentication required)</strong></summary>

| Tool | Description |
|---|---|
| `search_jobs` | Search remote jobs by keyword, country, experience, type, salary, benefits, skills, and more |
| `get_jobs` | Browse latest remote job listings |
| `get_job_details` | Full job description, salary, screening questions, and application link |
| `get_related_jobs` | Find similar jobs by skills, location, and category |
| `search_companies` | Search companies by keyword, country, benefits, tech stack |
| `get_companies` | Browse remote-friendly companies |
| `get_company_details` | Full company profile with tech stack, benefits, and open jobs |
| `get_salary_data` | Salary benchmarks by job title, seniority, and country (min/median/max USD) |
| `get_remote_work_statistics` | Top skills, categories, countries, and industries by remote job count |
| `search_talent` | Search 100K+ remote candidates by keyword, country, and skills |
| `get_correct_country_name` | Fuzzy-match country names to the correct format |
| `check_job_payment_status` | Check Stripe payment status for job postings |

</details>

<details>
<summary><strong>Job seeker tools (free Himalayas account required)</strong></summary>

| Tool | Description |
|---|---|
| `get_my_profile` | View your complete profile |
| `update_profile` | Update bio, location, search status, salary expectations, and more |
| `add_experience` | Add work experience with title, company, dates, skills |
| `add_education` | Add education with school, degree, field, years |
| `update_tech_stack` | Set technologies on your profile |
| `save_job` | Save a job to your kanban tracker with status, salary, excitement, notes |
| `get_saved_jobs` | View all saved jobs grouped by pipeline status |
| `update_job_status` | Move a job through your pipeline |
| `remove_saved_job` | Remove a job from your tracker |

</details>

<details>
<summary><strong>Employer tools (company account required)</strong></summary>

| Tool | Description |
|---|---|
| `get_company_profile` | View your company profile and open positions |
| `update_company_profile` | Update about, summary, CEO, employee range, locations, social links |
| `update_company_tech_stack` | Set your company's technologies (fuzzy-matched) |
| `get_company_perks` | View perks grouped by category |
| `add_company_perk` | Add a perk with title, category, and description |
| `remove_company_perk` | Remove a perk by ID |
| `create_company_job` | Post a remote job with screening questions and paid extras |
| `update_company_job` | Update any field of an existing posting |
| `delete_company_job` | Permanently delete a posting |
| `list_company_jobs` | List all jobs with views, clicks, status, and expiry |
| `show_company_job` | Full details of a specific posting |
| `purchase_job_extras` | Buy sticky or newsletter placement (returns Stripe checkout URL) |
| `post_job_public` | Post a job without an account (Stripe payment required) |

</details>

## Troubleshooting

**Connection issues** — Ensure Node.js is installed (`node --version`). Restart your AI assistant after configuration changes. Clear auth cache if needed: `rm -rf ~/.mcp-auth`.

**Authentication problems** — Complete the OAuth flow in the browser window that opens. Use the correct server URL: `https://mcp.himalayas.app/mcp`. For employer tools, ensure your Himalayas account is linked to a company.

**Tools not appearing** — Verify valid JSON syntax in your configuration file. Restart your AI assistant completely. Check the tools menu in your AI assistant's interface.

## Documentation

- [MCP Server Documentation](https://himalayas.app/docs/remote-jobs-mcp) — Full tool reference with parameters, examples, and AI agent instructions
- [How to Hire Remote Talent with AI](https://himalayas.app/docs/hire-with-ai) — Post jobs, search candidates, and benchmark salaries through AI
- [AI Agents Hub](https://himalayas.app/docs/ai-agents) — Overview of MCP, API, and RSS integrations
- [Data Dictionary](https://himalayas.app/docs/data-dictionary) — Every field, enum, and taxonomy
- [How to Post Jobs Using AI](https://himalayas.app/advice/how-to-post-jobs-using-ai) — Walkthrough of AI-powered job posting methods and best practices
- [Free Alternative to LinkedIn Recruiter](https://himalayas.app/advice/free-alternative-to-linkedin-recruiter) — How Himalayas talent search compares to LinkedIn Recruiter

## Support

For setup questions or integration support, email [hi@himalayas.app](mailto:hi@himalayas.app).

---

**Powered by [Himalayas.app](https://himalayas.app)** — The remote jobs marketplace
