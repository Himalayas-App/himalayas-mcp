# Himalayas Remote Jobs MCP Server

Remote jobs: job search, salary data and application tracking, or post a job and hire candidates.

**Server URL:** `https://mcp.himalayas.app/mcp` (Streamable HTTP)

The Himalayas MCP server connects AI assistants to the [Himalayas](https://himalayas.app) remote jobs marketplace in real time. It has 79 tools: 13 public tools that need no account, 46 tools for job seekers and 20 tools for employers. Sign-in uses OAuth in your browser. There is no API key, and clients with native remote MCP support need no Node.js and no `mcp-remote`.

The old SSE endpoint (`/sse`) is retired and returns `410 Gone`.

## What you can do

**Job seekers**

- "Find remote Python developer jobs paying over $150K that I can do from Canada"
- "What does a senior data engineer earn in Germany?"
- "Show me new jobs that match my profile since last week"
- "Write a resume and cover letter for this job, then give me the apply link"
- "Move the Stripe application to interviewing"
- "Reply to the recruiter in my inbox"

**Employers**

- "Post a remote Senior Frontend Engineer role at $140-170K, full-time, worldwide"
- "Show me how our job postings are performing"
- "Find React developers in Canada who are open to new roles"
- "Message this candidate about our React role"

Jobs are free to post and are reviewed before they go live. Optional paid extras (sticky placement, newsletter feature) return a Stripe checkout link. Companies without a Himalayas account can post a paid job with `post_job_public`. For the employer workflow, see [How to Hire Remote Talent with AI](https://himalayas.app/docs/hire-with-ai).

## Setup

Use the server URL `https://mcp.himalayas.app/mcp` in any client that supports remote MCP servers. Public tools work as soon as you connect. The first time you use a tool that needs an account, the client opens a Himalayas sign-in page.

### Claude (claude.ai and Claude Desktop)

1. Go to **Customize > Connectors**.
2. Click **+ Add**, then **Add custom connector**.
3. Enter the name `Himalayas` and the URL `https://mcp.himalayas.app/mcp`, then follow the prompts.

On Team and Enterprise plans, an Owner adds the connector in **Organization settings > Connectors**, then each member connects it from **Customize > Connectors**.

### Claude Code

```bash
claude mcp add --transport http himalayas https://mcp.himalayas.app/mcp
```

Then run `/mcp` inside Claude Code to sign in when you need account tools.

### ChatGPT

1. Open [ChatGPT Plugins](https://chatgpt.com/plugins).
2. Select **+**, then **Add custom MCP server**.
3. Enter the name `Himalayas` and the URL `https://mcp.himalayas.app/mcp`, choose OAuth, and confirm.

Your account or workspace policy decides whether you can add custom MCP servers.

### Cursor

Add to `~/.cursor/mcp.json` (or `.cursor/mcp.json` in a project):

```json
{
  "mcpServers": {
    "himalayas": {
      "url": "https://mcp.himalayas.app/mcp"
    }
  }
}
```

### VS Code

Add to `.vscode/mcp.json` in your workspace:

```json
{
  "servers": {
    "himalayas": {
      "type": "http",
      "url": "https://mcp.himalayas.app/mcp"
    }
  }
}
```

### Windsurf (Devin Desktop)

Add to your `mcp_config.json` (open it from the MCP settings in Cascade):

```json
{
  "mcpServers": {
    "himalayas": {
      "serverUrl": "https://mcp.himalayas.app/mcp"
    }
  }
}
```

### Gemini CLI

Install the Himalayas extension:

```bash
gemini extensions install https://github.com/Himalayas-App/himalayas-plugin
```

Or add the server to `~/.gemini/settings.json`:

```json
{
  "mcpServers": {
    "himalayas": {
      "httpUrl": "https://mcp.himalayas.app/mcp"
    }
  }
}
```

### Other clients

Any MCP client with Streamable HTTP support can connect to `https://mcp.himalayas.app/mcp`.

For a client that only runs local (stdio) servers, use `mcp-remote` as a bridge. This needs Node.js:

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

### Plugins

The [Himalayas plugin](https://github.com/Himalayas-App/himalayas-plugin) adds this server plus commands and skills for job seekers and employers.

- **Claude Code:** `/plugin marketplace add Himalayas-App/himalayas-plugin`, then `/plugin install himalayas@himalayas`
- **Gemini CLI:** `gemini extensions install https://github.com/Himalayas-App/himalayas-plugin`
- **Codex, Cursor and Grok:** load the repository as a plugin

## Authentication

Public tools need no account: job search and job details, related jobs, companies, salary data, remote work statistics, the country name helper, feedback, and public job posting with its payment check.

Every other tool needs a free Himalayas account. That includes talent search (`search_talent` and `get_talent_profile`): an anonymous call returns "Authentication required". Employer tools also need an account linked to a company.

Sign-in uses OAuth 2.1 with PKCE (S256). Clients can identify themselves with a Client ID Metadata Document, or register dynamically with a loopback redirect URI. You sign in on himalayas.app, so the client never sees your password, and each connection only gets the scopes you approve. Tokens refresh automatically.

## Tool Reference

79 tools, from the server's live `tools/list`.

<details>
<summary><strong>Public tools (13, no account needed)</strong></summary>

| Tool | Purpose |
|---|---|
| `search_jobs` | Search remote jobs by title, skill or keyword, with filters for country, worldwide, seniority, employment type, salary, markets, benefits and companies |
| `get_jobs` | Browse the latest remote jobs, optionally by country or worldwide |
| `get_job_details` | Full details for one job, including description, requirements and salary |
| `get_related_jobs` | Jobs similar to a given job, by skills, location and category |
| `search_companies` | Search remote-friendly companies by keyword, optionally by country |
| `get_companies` | Browse remote-friendly companies, optionally by country or worldwide |
| `get_company_details` | Company profile with about, tech stack, benefits, open jobs and social links |
| `get_salary_data` | Salary benchmarks by job title, with optional seniority and country (min, median and max in USD) |
| `get_remote_work_statistics` | Top skills, job categories, industries or countries by job or company count |
| `get_correct_country_name` | Resolve a country name to the format Himalayas filters accept |
| `submit_feedback` | Send a problem report to the Himalayas engineering team |
| `post_job_public` | Post a paid job without an account; returns a Stripe checkout link |
| `check_job_payment_status` | Check a job posting's payment status by checkout session id |

</details>

<details>
<summary><strong>Job seeker tools (46, free account)</strong></summary>

| Tool | Purpose |
|---|---|
| `get_new_matches` | Jobs matching your profile posted since the last check, leaving out jobs already in your tracker |
| `skip_job` | Pass on a job with a reason so it stops coming back in new matches |
| `get_apply_link` | The employer's application link for a job you have decided to apply to (50 links per account per day) |
| `generate_application_documents` | Write a resume and cover letter tailored to a Himalayas job from your profile |
| `save_job` | Save a job to your application tracker |
| `get_saved_jobs` | List every job in your tracker with status, outcome, salary, notes and links |
| `update_job_status` | Update a tracked job's status, outcome or details |
| `remove_saved_job` | Remove a job from your tracker |
| `list_saved_answers` | List your saved answers to job application questions |
| `update_saved_answer` | Change the text of a saved application answer |
| `delete_saved_answer` | Delete a saved application answer |
| `get_my_profile` | Get your Himalayas profile |
| `update_profile` | Update your Himalayas profile |
| `import_profile` | Fill in your profile from a LinkedIn profile URL or resume text |
| `add_experience` | Add a work experience to your profile |
| `update_experience` | Edit a work experience by id |
| `delete_experience` | Delete a work experience by id |
| `add_education` | Add an education entry to your profile |
| `update_education` | Edit an education entry by id |
| `delete_education` | Delete an education entry by id |
| `update_tech_stack` | Set the tools and technologies on your profile |
| `update_profile_photo` | Set your profile photo or cover photo from an image URL |
| `list_headshots` | List the AI headshots you have made |
| `use_headshot_as_profile_photo` | Set one of your AI headshots as your profile photo |
| `get_headshots_link` | Link to the page where you make AI headshots |
| `get_verification_link` | Next step for verifying your identity and work permits (the verified badge) |
| `list_documents` | List your tailored resumes and cover letters |
| `get_document` | Read one tailored resume or cover letter |
| `update_document` | Rename a document, or replace a cover letter's text |
| `delete_document` | Delete a tailored resume or cover letter |
| `list_interviews` | List your interview practice, with links to practise again and the minutes and credits left |
| `get_interview_results` | Scores and feedback from your interview practice for one job |
| `get_interview_practice_link` | Link to practise a mock interview for a specific job |
| `list_coach_chats` | List your career coach conversations |
| `get_coach_chat` | Read one career coach conversation |
| `list_my_conversations` | List your inbox: conversations companies and recruiters started with you |
| `get_my_conversation` | Read the latest messages in one inbox conversation |
| `reply_to_message` | Reply in an inbox conversation |
| `mark_my_message_read` | Mark an inbox message as read |
| `list_notifications` | List your newest notifications |
| `mark_notifications_read` | Mark one or all notifications as read |
| `update_email_preferences` | Turn Himalayas emails on or off |
| `update_account` | Change your account time zone |
| `get_plus_checkout_link` | Stripe checkout link for Himalayas Plus (US$9 a month) |
| `get_billing_portal_link` | Link to your Stripe billing page, for users who have paid before |
| `join_radar_waitlist` | Join the waitlist for Himalayas Radar |

</details>

<details>
<summary><strong>Employer tools (20, account required)</strong></summary>

`search_talent` and `get_talent_profile` work with any signed-in account. The other employer tools need an account linked to a company.

| Tool | Purpose |
|---|---|
| `search_talent` | Search remote candidates by skill, job title or keyword and country |
| `get_talent_profile` | Full candidate profile with bio, experience, education, tech stack and social links |
| `get_company_profile` | Get your company's profile |
| `update_company_profile` | Update your company's profile |
| `update_company_tech_stack` | Set your company's tech stack |
| `get_company_perks` | Get your company's perks and benefits |
| `add_company_perk` | Add a perk or benefit |
| `remove_company_perk` | Remove a perk or benefit |
| `create_company_job` | Post a remote job, or save it as a draft (free, reviewed before it goes live) |
| `update_company_job` | Update an existing job posting |
| `delete_company_job` | Delete a job posting |
| `list_company_jobs` | List your job postings with status, views, clicks and expiry |
| `show_company_job` | Full details of one of your job postings |
| `purchase_job_extras` | Buy sticky placement or a newsletter feature for a job; returns a Stripe checkout link |
| `list_conversations` | List your conversations with candidates |
| `get_conversation` | Get the message history for a conversation |
| `start_conversation` | Start a conversation with a candidate |
| `send_message` | Send a message in an existing conversation |
| `mark_message_read` | Mark a message as read |
| `delete_conversation` | Delete a conversation |

</details>

## Troubleshooting

**Account tools ask you to sign in again.** Finish the sign-in in the browser window the client opens. In Claude Code, run `/mcp` and choose the Himalayas server.

**"Authentication required".** The tool needs a Himalayas account. Connect your account through your client's sign-in flow. Talent search needs an account too.

**Employer tools say there is no company.** Your Himalayas account needs to be linked to a company.

**Tools don't appear.** Check that the URL is exactly `https://mcp.himalayas.app/mcp` and that your config file is valid JSON, then restart the client or reload its MCP servers.

## Documentation

- [MCP Server Documentation](https://himalayas.app/docs/remote-jobs-mcp): setup, tool parameters, examples and AI agent instructions
- [How to Hire Remote Talent with AI](https://himalayas.app/docs/hire-with-ai): post jobs, search candidates and benchmark salaries through AI
- [AI Agents Hub](https://himalayas.app/docs/ai-agents): overview of the MCP server, API and RSS feed
- [Data Dictionary](https://himalayas.app/docs/data-dictionary): every field, enum and taxonomy
- [How to Post Jobs Using AI](https://himalayas.app/advice/how-to-post-jobs-using-ai): ways to post jobs with AI
- [Free Alternative to LinkedIn Recruiter](https://himalayas.app/advice/free-alternative-to-linkedin-recruiter): how Himalayas talent search compares to LinkedIn Recruiter
- [Privacy policy](https://himalayas.app/privacy)

## Other ways to access Himalayas job data

The MCP server is the best fit for AI assistants and agents, since it queries live data and exposes tools for jobs, companies, salaries, candidates, and applications. For everything else:

| | MCP server | [JSON API](https://github.com/Himalayas-App/remote-jobs-api) | [RSS feed](https://github.com/Himalayas-App/remote-jobs-rss-feed) |
| --- | --- | --- | --- |
| **Interface** | MCP tools | REST + JSON | RSS 2.0 XML |
| **Coverage** | All jobs, plus companies, salaries, and talent | All jobs, paginated | Latest 100 jobs |
| **Freshness** | Real time | Every 24 hours | Every 24 hours |
| **Auth** | None for public tools; OAuth for account tools | None | None |
| **Best for** | AI assistants and agents | Apps, databases, backfilling a job board | Feed readers, monitoring, no-code automations |

- **[Remote Jobs API](https://github.com/Himalayas-App/remote-jobs-api)**: free public JSON API with browse and search endpoints, an OpenAPI 3.1 spec, and runnable examples in curl, Python, Node.js, TypeScript, PHP, Go, and Ruby.
- **[Remote Jobs RSS Feed](https://github.com/Himalayas-App/remote-jobs-rss-feed)**: the 100 most recent listings as XML, with parsing examples in five languages and recipes for Slack, Zapier, and n8n.
- **[Embeddable widget](https://himalayas.app/free-remote-jobs-widget)**: live remote job listings on any web page with one line of code.

## Support

For setup questions or integration support, email [hi@himalayas.app](mailto:hi@himalayas.app).

---

**Powered by [Himalayas.app](https://himalayas.app)**, the remote jobs marketplace.
