# AI Visibility Check MCP server

Audit how AI assistants and search engines find, understand and recommend a
website, from inside Claude, ChatGPT, Cursor, VS Code or any other MCP client.

[AI Visibility Check](https://aivisibilitycheck.io) is a hosted service. This
repository holds no code: it describes the remote MCP server at

```
https://aivisibilitycheck.io/mcp
```

for the [MCP Registry](https://registry.modelcontextprotocol.io) (`server.json`)
and for the people connecting to it (this file). There is nothing to install.

- **Transport:** Streamable HTTP
- **Sign-in:** OAuth 2.1 with PKCE and dynamic client registration. Your client
  opens our sign-in page; a free account can be created there.
- **Registry name:** `io.aivisibilitycheck/mcp`

## What it does

Ask your assistant to audit a website and it runs the audit on your account,
then answers questions about the result: what is wrong, what to fix first,
and whether AI assistants recommend the business.

- **Quick audit:** checks the homepage in about a minute. Free.
- **Full audit:** crawls the site, renders it in a real browser, checks
  outside sources and asks AI models about the brand. Takes about seven
  minutes and uses one full audit from your account's allowance, so the
  server tells the assistant to check with you before starting one. A site
  that had a full audit in the last day gets that report back instead of a
  new run, unless you ask for a new one.

A new account comes with three full audits and gets one more each month.
Nothing is sold through the MCP server: its answers never contain a price or
a payment link.

## Connect

### Claude

1. **Settings → Connectors → Add custom connector**.
2. Name: `AI Visibility Check`, Remote MCP server URL:
   `https://aivisibilitycheck.io/mcp`.
3. **Add**, then **Connect**, and sign in on the page that opens.

Step by step: [aivisibilitycheck.io/claude-connector](https://aivisibilitycheck.io/claude-connector/)

### ChatGPT

1. **Apps → Add → Create**, if your plan allows custom apps.
2. Name: `AI Visibility Check`, Server URL:
   `https://aivisibilitycheck.io/mcp`, Authentication: OAuth.
3. Confirm and sign in on the page that opens.

Step by step: [aivisibilitycheck.io/chatgpt-app](https://aivisibilitycheck.io/chatgpt-app/)

### Claude Code

```bash
claude mcp add --transport http aivisibilitycheck https://aivisibilitycheck.io/mcp
```

Then run `/mcp` in Claude Code and choose **Authenticate**.

### Cursor

`~/.cursor/mcp.json`, or `.cursor/mcp.json` in a project:

```json
{
  "mcpServers": {
    "aivisibilitycheck": {
      "url": "https://aivisibilitycheck.io/mcp"
    }
  }
}
```

### VS Code

`.vscode/mcp.json`:

```json
{
  "servers": {
    "aivisibilitycheck": {
      "type": "http",
      "url": "https://aivisibilitycheck.io/mcp"
    }
  }
}
```

### Other clients

Any client that speaks Streamable HTTP and MCP's OAuth flow can connect to
`https://aivisibilitycheck.io/mcp`. It discovers the sign-in server from
`https://aivisibilitycheck.io/.well-known/oauth-protected-resource/mcp`.

## What to ask

- "Run a quick AI visibility audit of example.com."
- "Run a full audit of example.com for the keywords plumber leeds and emergency plumber."
- "What are the critical issues?"
- "Show me the structured data section."
- "What should I fix first, and how much would it raise the score?"
- "Do AI assistants recommend this business? Which competitors do they name instead?"
- "How many full audits do I have left?"

## Tools

| Tool | What it does | Changes anything? |
| --- | --- | --- |
| `start_site_audit` | Starts a quick or full audit of a web address | Starts an audit; a full one uses one from the allowance |
| `get_site_audit` | Progress, or the score, headline, top five actions and report link | No |
| `list_site_audits` | Your recent audits, optionally for one domain | No |
| `check_audit_allowance` | Full audits left, when they expire, when the next free one comes | No |
| `get_audit_issues` | Problems found, most important first, by severity or section | No |
| `get_audit_section` | Every check in one part of an audit, with its evidence | No |
| `get_action_plan` | What to fix, in order, with effort and score gain | No |
| `get_ai_visibility` | Whether AI models recognise and recommend the brand, and who they name instead | No |

## What it can access

Once you allow the connection, your client can start audits and read your
audits and their results, your email address and your remaining allowance.
It cannot buy anything, change your plan or payment details, or delete
anything.

Disconnect any time with **Disconnect** under *Connected apps* on your
[account page](https://aivisibilitycheck.io/account), or by removing the
server from your client. Access ends within a minute.

What you ask your assistant, and the results sent back to it, are also
processed by that assistant's provider under its own terms. Our
[privacy notice](https://aivisibilitycheck.io/privacy/) covers what we do
with your data; using the service means agreeing to our
[terms](https://aivisibilitycheck.io/terms/).

## Support

[info@cyberspark.uk](mailto:info@cyberspark.uk). Report a problem with this
listing as a GitHub issue.

AI Visibility Check is made by [Cyber Spark IT Services LTD](https://cyberspark.uk)
(company number 14891489).
