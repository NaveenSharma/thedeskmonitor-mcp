# TheDeskMonitor MCP Server

[![MCP Protocol](https://img.shields.io/badge/MCP-2025--11--25-blue)](https://modelcontextprotocol.io)
[![Transport](https://img.shields.io/badge/transport-streamable--http-green)](https://thedeskmonitor.com/integrations/ai-connect)
[![Auth](https://img.shields.io/badge/auth-OAuth%202.1%2FPKCE-orange)](https://thedeskmonitor.com/integrations/ai-connect)

A remote **Model Context Protocol (MCP) server** for [TheDeskMonitor](https://thedeskmonitor.com) — a workforce analytics, time tracking, and productivity monitoring platform for SMBs. Connect any MCP-compatible AI assistant (Claude Desktop, Cursor, Windsurf, etc.) to your workforce data.

---

## What It Does

TheDeskMonitor's MCP server exposes 24 tools across six functional categories, allowing AI assistants to:

- Check who is currently clocked in and their attendance status
- Summarise team hours, workload, and productivity metrics
- Browse the employee directory and retrieve individual profiles
- Manage timesheet approvals
- Get dashboard analytics and overviews
- Explore pricing, start a free trial, or switch to a read-only demo tenant

---

## MCP Server Details

| Property | Value |
|---|---|
| **MCP Server URL** | `https://api.thedeskmonitor.com/api/mcp/v1/` |
| **Transport** | Streamable HTTP (MCP protocol version 2025-11-25) |
| **Auth** | OAuth 2.1 / PKCE — RFC 9728 + RFC 8414 compliant |
| **Tool count** | 24 tools |
| **Demo mode** | Public key `dm_demo_public_v1` — read-only, no account required |

### OAuth discovery endpoints

```
GET https://api.thedeskmonitor.com/.well-known/oauth-authorization-server
GET https://api.thedeskmonitor.com/.well-known/oauth-protected-resource
```

---

## Tools

### Attendance & Time

| Tool | Description |
|---|---|
| `clock_in` | Clock the authenticated user in |
| `clock_out` | Clock the authenticated user out |
| `list_my_timesheet` | List the current user's timesheet entries |
| `list_pending_approvals` | List timesheets awaiting manager approval |

### Analytics & Productivity

| Tool | Description |
|---|---|
| `get_dashboard_summary` | High-level productivity and attendance summary for the tenant |
| `summarize_team_hours` | Aggregate hours by team/department for a date range |
| `get_workload_alerts` | Identify overloaded or underutilised employees |
| `get_productivity_overview` | Productivity scores and trends |
| `list_recent_activity` | Recent events across the tenant |
| `get_analytics_overview` | Overview of analytics data |
| `get_analytics_feature_usage` | Feature adoption and usage metrics |
| `get_analytics_questions` | Common analytics questions and answers |

### Employee Directory

| Tool | Description |
|---|---|
| `list_employees` | List all employees in the tenant |
| `get_employee_details` | Retrieve full profile for a specific employee |
| `invite_staff` | Invite a new staff member to the tenant |

### Product & Onboarding

| Tool | Description |
|---|---|
| `get_capabilities` | List all available MCP tools and their capabilities |
| `get_started_guide` | Getting started guide for new users |
| `get_data_dictionary` | Data field definitions and schema reference |
| `get_pricing_and_plans` | Current pricing tiers and plan features |
| `start_free_trial` | Initiate a free trial for a new tenant |
| `get_demo_scenarios` | Browse available demo scenarios |
| `switch_to_demo` | Switch the session to the read-only demo tenant |
| `switch_to_production` | Switch back from demo to the production tenant |
| `ask_workforce` | Natural-language workforce query interface |

---

## Connecting via Claude Desktop

Add the following to your `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "thedeskmonitor": {
      "type": "http",
      "url": "https://api.thedeskmonitor.com/api/mcp/v1/",
      "oauth": {
        "authorizationUrl": "https://api.thedeskmonitor.com/oauth/authorize",
        "tokenUrl": "https://api.thedeskmonitor.com/oauth/token",
        "scopes": ["mcp"]
      }
    }
  }
}
```

For a read-only demo (no account needed), use the public demo key:

```json
{
  "mcpServers": {
    "thedeskmonitor-demo": {
      "type": "http",
      "url": "https://api.thedeskmonitor.com/api/mcp/v1/",
      "headers": {
        "Authorization": "Bearer dm_demo_public_v1"
      }
    }
  }
}
```

---

## Connecting via Other MCP Clients

Any MCP client that supports Streamable HTTP transport and OAuth 2.1 can connect. Point it at:

```
https://api.thedeskmonitor.com/api/mcp/v1/
```

The server advertises its OAuth metadata at `/.well-known/oauth-authorization-server`, so compliant clients can auto-discover auth parameters.

---

## Links

- **Product site**: https://thedeskmonitor.com
- **AI Connect page**: https://thedeskmonitor.com/integrations/ai-connect
- **AI Commands reference**: https://thedeskmonitor.com/ai-commands
- **Glama listing**: https://glama.ai/mcp/connectors/com.thedeskmonitor/mcp

---

## License

MIT — see [LICENSE](LICENSE)

---

## Contributing

This repository is the public discovery artifact for TheDeskMonitor's remote MCP server. The server itself is hosted at `api.thedeskmonitor.com`.

If you encounter an issue connecting an MCP client, or would like a tool added, please open a GitHub issue with:

1. The MCP client you are using (name and version)
2. The tool or capability you expected
3. The error or unexpected behaviour you observed

We review issues and respond within a few business days.
