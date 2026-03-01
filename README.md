# Himalayas Remote Jobs MCP Server

Access remote job listings, salary data, company profiles, and career tools directly from your AI assistant. The Himalayas MCP server provides real-time tools for job search, company research, salary benchmarks, profile management, application tracking, and employer job posting. Works with any AI platform that supports MCP servers, including Claude (Desktop, Code, Cowork), ChatGPT, Gemini, Cursor, Windsurf, VS Code, Openclaw, and Microsoft Copilot Studio.

**Server URL (Streamable HTTP — recommended):** `https://mcp.himalayas.app/mcp`

**Server URL (SSE — legacy fallback):** `https://mcp.himalayas.app/sse`

[![Trust Score](https://archestra.ai/mcp-catalog/api/badge/quality/Himalayas-App/himalayas-mcp)](https://archestra.ai/mcp-catalog/himalayas-app__himalayas-mcp)

## Available Tools

### Public Tools (No Authentication Required)

#### Job Search & Discovery

**`search_jobs`** — Search remote jobs with comprehensive filtering.

| Parameter | Type | Description |
|---|---|---|
| keyword | string | Search term for job title, skills, or description |
| page | integer | Page number for pagination (default: 1) |
| country | string | Filter by country (e.g., "United States", "Germany") |
| worldwide | boolean | Show only jobs with no location restrictions |
| exclude_worldwide | boolean | Exclude worldwide jobs, show country-specific only |
| experience | string | entry-level, mid-level, senior, manager, director, executive |
| type | string | Full Time, Part Time, Contractor, Temporary, Intern, Volunteer, Other |
| salary_min | integer | Minimum salary filter |
| salary_max | integer | Maximum salary filter |
| currency | string | Salary currency (USD, EUR, GBP, CAD, AUD, and 20+ others) |
| salary_required | boolean | Only show jobs with salary information |
| markets | string | Filter by job categories/markets |
| benefits | string | Filter by company benefits |
| companies | string | Filter by specific company names |
| sort | string | relevant, recent, salaryAsc, salaryDesc |

**`get_jobs`** — Browse the latest remote job listings with optional country/worldwide filters.

**`get_job_details`** — Full job description, requirements, salary, screening questions, and application link. Parameters: company_slug, job_slug.

**`get_related_jobs`** — Find similar jobs by skills, location, and category. Parameters: company_slug, job_slug, page.

#### Company Research

**`search_companies`** — Search companies by keyword, country, benefits, tech_stack, sort (relevant, recent, jobs, nameAToZ, nameZToA).

**`get_companies`** — Browse remote-friendly companies with optional country/worldwide filters.

**`get_company_details`** — Comprehensive company profile: about, founded year, employee count, tech stack, benefits, open jobs, social links.

#### Salary Data & Market Intelligence

**`get_salary_data`** — Salary benchmarks by job title, seniority, and country. Returns min/median/max in USD. Fuzzy-matches job titles.

**`get_remote_work_statistics`** — Top 30 entries for skills, categories, countries, or industries by remote job/company count.

#### Talent Search

**`search_talent`** — Search remote candidates by keyword, country, page, sort. Returns profiles with name, current role, salary expectations, and search status.

#### Utility

**`get_correct_country_name`** — Fuzzy-match country name strings to the correct format for filtering.

**`check_job_payment_status`** — Check Stripe payment status for job postings by session ID.

### Job Seeker Tools (Requires Free Himalayas Account)

#### Profile Management

**`get_my_profile`** — View your complete profile: name, email, location, career preferences, experience, education, tech stack.

**`update_profile`** — Update bio, intro, location, career_search_status (actively_searching/open_to_roles/closed_to_roles), career_primary_role, salary expectations, career_description.

**`add_experience`** — Add work experience: title, company_name, employment_type, description, location, dates, skills.

**`add_education`** — Add education: school, degree, field, years, description.

**`update_tech_stack`** — Set up to 5 technologies on your profile (e.g., React, Python, TypeScript).

#### Job Application Tracker

**`save_job`** — Save a job to your kanban tracker with status, salary, excitement (0-5), notes, and links.

**`get_saved_jobs`** — View all saved jobs grouped by status (saved, applied, interviewing, negotiation, hired, archived).

**`update_job_status`** — Move a job through your pipeline or update notes/excitement.

**`remove_saved_job`** — Remove a job from your tracker.

### Employer Tools (Requires Company Account)

#### Company Profile

**`get_company_profile`** — View your company's profile and open positions count.

**`update_company_profile`** — Update about, summary, CEO, employee range, year founded, locations, social links.

**`update_company_tech_stack`** — Set your company's technologies (fuzzy-matched).

#### Perks & Benefits

**`get_company_perks`** — View perks grouped by category.

**`add_company_perk`** — Add a perk with title, category (10 categories), and description.

**`remove_company_perk`** — Remove a perk by ID.

#### Job Management

**`create_company_job`** — Post a remote job. Free to post, admin review required. Supports screening questions (boolean, text, multiple choice) and paid extras (sticky $199, newsletter $99).

**`update_company_job`** — Update any field of an existing posting.

**`delete_company_job`** — Permanently delete a posting.

**`list_company_jobs`** — List all jobs with status, views, clicks, and expiry.

**`show_company_job`** — Full details of a specific posting.

**`purchase_job_extras`** — Buy sticky or newsletter placement. Returns Stripe checkout URL.

### Public Job Posting (No Account Required)

**`post_job_public`** — Post a job without a Himalayas account. Provide email, company name, company URL, and job details. Email domain must match company URL. Stripe payment required.

## Setup Instructions

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
4. Public tools work immediately. For authenticated tools, you'll be prompted to log in on first use.

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

### Other MCP Clients

The Himalayas MCP server works with any MCP-compatible client including VS Code, Zed, Cline, Continue, and others. Connect to `https://mcp.himalayas.app/mcp` (Streamable HTTP) or `https://mcp.himalayas.app/sse` (SSE fallback).

## Example Conversations

### Job Search
- "Find remote Python developer jobs paying over $150K"
- "Show me senior React positions in Canada"
- "Search for part-time contractor roles worldwide"
- "What are the latest remote data science jobs?"

### Salary Research
- "What's the average salary for a Senior Product Manager?"
- "Compare salaries for React developers in the US vs Canada"
- "Show me salary benchmarks for DevOps engineers"

### Company Research
- "Tell me about Stripe's remote work setup"
- "Find companies that use React and offer unlimited PTO"
- "Which companies in Germany are hiring remotely?"

### Talent Sourcing (Employers)
- "Find React developers in Canada who are open to new roles"
- "Search for senior engineers with Python experience"

### Job Posting (Employers)
- "Post a remote Senior Frontend Engineer role at $140-170K"
- "Create a job listing for a Part-time Customer Support Specialist"
- "Show me how our job postings are performing"

### Profile & Tracking (Job Seekers)
- "Update my profile to actively searching"
- "Save this job to my application tracker"
- "Move the Stripe application to interviewing stage"
- "Add my new role at Acme Corp to my experience"

## Authentication

Public tools (job search, salary data, company research, talent search) work without any authentication.

Authenticated tools use **OAuth 2.1 with PKCE**. When you first use a profile, tracker, or employer tool, your AI assistant will open a secure login page in your browser. Log in with your Himalayas account, and your session persists with automatic token refresh.

## Troubleshooting

### Connection Issues
- Ensure Node.js is installed (`node --version`)
- Try restarting your AI assistant after configuration changes
- Clear auth cache if needed: `rm -rf ~/.mcp-auth`

### Authentication Problems
- Complete the OAuth flow in the browser window that opens
- Use the correct server URL: `https://mcp.himalayas.app/mcp`
- For employer tools, ensure your Himalayas account is associated with a company

### Tools Not Appearing
- Verify valid JSON syntax in your configuration file
- Restart your AI assistant completely
- Check the tools menu in your AI assistant's interface

## Documentation

- [MCP Server Documentation](https://himalayas.app/docs/remote-jobs-mcp) — Full tool reference with parameters, examples, and AI agent instructions
- [Hire with AI](https://himalayas.app/docs/hire-with-ai) — Post jobs, search candidates, and benchmark salaries through AI conversation
- [AI Agents Hub](https://himalayas.app/docs/ai-agents) — Overview of MCP, API, and RSS integrations
- [Data Dictionary](https://himalayas.app/docs/data-dictionary) — Every field, enum, and taxonomy

## Support

For setup questions or integration support, email [hi@himalayas.app](mailto:hi@himalayas.app).

---

**Powered by [Himalayas.app](https://himalayas.app)** — The remote jobs marketplace
