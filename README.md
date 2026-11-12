---
title: TERCEPT MCP Server
---

<h1 style="display:flex;align-items:center;gap:12px"><img src="assets/images/tercept-icon.png" alt="" width="44" height="44">TERCEPT MCP Server</h1>

Connect your AI assistant to your TERCEPT account. Ask questions about your data, find dashboards and charts, run
read-only SQL and manage scheduled reports, all in plain language.

| At a glance | |
|---|---|
| **Server URL** | https://insights-mcp.tercept.com/mcp |
| **Sign-in** | OAuth 2.0 with your TERCEPT login |
| **Who can use it** | TERCEPT users whose admin has turned on MCP access |
| **Support** | [support@tercept.com](mailto:support@tercept.com) |

## Contents

1. [What the TERCEPT MCP Server does](#what-the-tercept-mcp-server-does)
2. [How it works](#how-it-works)
3. [Before you start](#before-you-start)
4. [Connect your assistant](#connect-your-assistant)
5. [Tools](#tools)
6. [Example prompts](#example-prompts)
7. [Limits](#limits)
8. [Troubleshooting](#troubleshooting)
9. [Support](#support)

---

## What the TERCEPT MCP Server does

TERCEPT is an analytics and reporting platform. Customers use it to bring together data from their ad platforms,
marketplaces and other sources, and to build reports and dashboards on top of it.

The TERCEPT MCP Server connects your TERCEPT account to your AI assistant. Once connected, you can:

- Find dashboards, charts, data sources and saved queries, and ask what they show.
- Ask questions about your numbers. The assistant reads chart data, or writes and runs a read-only SQL query, to answer.
- Get a link to a new chart in Explore, ready to adjust and save.
- Open a query in SQL Lab to continue working on it.
- Create, change or delete scheduled reports and alerts, and preview an alert email before you create it.
- Get help with TERCEPT features and menus.

> **Example:** You ask your assistant, "How did revenue by demand partner change last week compared with the week
> before?" It finds the right data source in your TERCEPT account, checks its columns and metrics, runs a read-only
> query for both weeks and gives you the comparison along with the figures it used.

## How it works

1. You connect the server once and sign in with your TERCEPT login.
2. When you ask a question, the assistant chooses the tools it needs, for example listing your data sources and then
   running a SQL query.
3. Each tool runs in TERCEPT as you, using your TERCEPT permissions, and returns the result to the assistant.
4. The assistant uses those results to answer you.

**Good to know**

- The assistant only knows what the tools return. The tools only list dashboards, charts and data sources that your
  TERCEPT account can open.
- Clear questions get better answers. Naming the dashboard, data source, metric or date range you mean helps.
- If you don't give a date range for a large table, the assistant uses the data source's default window, or the last
  30 days.
- SQL access is read-only. Any query that would change data is refused.

## Before you start

You sign in on insights.tercept.com with the same login you use for TERCEPT: username and password, or Google sign-in
if your company uses it. Your password is never shared with the assistant.

Your TERCEPT admin controls who can use the server and what they can do:

| To do this | Your account needs |
|---|---|
| Connect | MCP access, turned on by your TERCEPT admin |
| View dashboards, charts and data sources | Access to them in TERCEPT |
| Run SQL queries | SQL Lab access, and access to the data you query |
| Create and manage scheduled reports and alerts | MCP access only |

TERCEPT admins also have tools for creating and editing charts, dashboards and datasets. These tools are not shown to
other users.

## Connect your assistant

All users connect to the same server URL:

```
https://insights-mcp.tercept.com/mcp
```

The URL contains no key or password. Each user signs in separately with their own TERCEPT login.

### From your assistant's directory

If your assistant lists the **TERCEPT MCP Server** in its directory of apps or connectors:

1. Find **TERCEPT MCP Server** in the directory.
2. Click **Connect**. The TERCEPT sign-in page opens.
3. Sign in. You are returned to your assistant.
4. Turn the server on in the conversations where you want to use it, if your assistant asks you to.

### By URL

If your assistant lets you add an MCP server by URL (often called a custom connector or custom app):

1. Add a new MCP server or connector.
2. Enter **TERCEPT MCP Server** as the name and the server URL above.
3. Choose OAuth if the assistant asks how to authenticate.
4. Connect and sign in with your TERCEPT login.

Any MCP client that supports remote servers over HTTP with OAuth sign-in can connect this way.

### Disconnecting

Remove the server from your assistant's connector or app settings. Your TERCEPT admin can also remove your MCP
access, which stops all tool calls immediately.

## Tools

### Read-only tools

| Area | Tool | What it does |
|---|---|---|
| Dashboards | list_dashboards | Lists the dashboards you can access |
| | get_dashboard_info | Shows a dashboard's details and the charts on it |
| Charts | list_visualizations | Lists the charts you can access |
| | get_visualization_info | Shows a chart's details and settings |
| | get_visualization_data | Returns the data behind a chart |
| | get_visualization_preview | Returns a preview of a chart |
| | get_chart_type_schema | Describes the settings a chart type accepts |
| Data sources | list_data_sources | Lists the data sources you can access |
| | get_data_source_info | Shows a data source's columns, metrics and notes |
| | list_source_metrics_columns | Lists the metrics and calculated columns on a data source |
| | preview_column_change | Previews a change to a calculated column without saving it |
| | preview_metric_change | Previews a change to a metric without saving it |
| Connections | list_connections | Lists the database connections you can access |
| | get_connection_info | Shows a connection's details |
| SQL | execute_sql | Runs a read-only SQL query and returns the results |
| | open_sql_lab_with_context | Opens SQL Lab with a query filled in |
| | list_queries, get_query_info | Lists your recent queries and their details |
| | list_saved_queries, get_saved_query_info | Lists saved queries and their details |
| Reports and alerts | list_reports, get_report_info | Lists scheduled reports and alerts and their details |
| | list_report_logs, get_report_log_info | Shows when reports and alerts ran and whether they succeeded |
| | preview_alert_email | Shows what an alert email will look like, using current data |
| Help and account | get_platform_help | Answers questions about TERCEPT features and menus |
| | get_mcp_usage | Shows how much of your daily data limit you have used |
| | get_schema | Lists the fields you can filter and sort on |
| | health_check | Checks that the server is running |
| Other | list_tags, get_tag_info | Tags and their details |
| | list_annotation_layers, get_annotation_layer_info, list_layer_annotations, get_layer_annotation_info | Annotation layers and annotations |
| | list_roles, get_role_info, list_users, get_user_info | Roles and users (some details are visible to admins only) |

### Tools that make changes

| Tool | What it does |
|---|---|
| generate_explore_link | Creates a link to a new chart in Explore. Nothing is saved until you save it in TERCEPT |
| create_report | Creates a scheduled report or alert |
| update_report | Changes an existing report or alert |
| delete_report | Deletes a report or alert |

Depending on your assistant's settings, it asks for your approval before using a tool that makes changes.

## Example prompts

- "What dashboards do I have, and what does the Revenue Overview dashboard show?"
- "Show revenue and eCPM by demand partner for the last 30 days, highest revenue first."
- "Compare last week's fill rate with the week before for each site. Which site dropped the most?"
- "Give me a chart of daily revenue by device for the last 90 days that I can open in Explore."
- "Email me a report of yesterday's top 10 ad units by revenue every weekday at 9am."
- "How much of my daily data limit have I used today?"

## Limits

| Limit | What it means |
|---|---|
| **Rate limits** | Each user can call each tool a limited number of times per minute. If you reach the limit, wait a minute and try again. |
| **Daily data limit** | SQL queries count towards a daily limit on the amount of data your account can scan. The limit is set for your account, and you can ask the assistant how much you have used. |
| **Sign-in** | You stay signed in while you use the server. You are asked to sign in again after a period without use. |

## Troubleshooting

| Problem | Solution |
|---|---|
| "Couldn't reach the MCP server" or "Authorization failed" when connecting | Check that the URL is exactly https://insights-mcp.tercept.com/mcp and try again. If the problem continues, contact support and include the time it happened. |
| A message saying your account does not have MCP access | Ask your TERCEPT admin to turn on MCP access for your account. |
| A SQL query is refused | Only read-only queries are allowed. Running SQL also needs SQL Lab access and access to the data you query, which your admin can grant. |
| A rate limit or daily data limit message | Wait and try again, or narrow the question with a shorter date range or fewer columns. |
| The answer does not match a dashboard | Dashboards often apply filters. Name the chart and ask the assistant to use that chart's data, or check the dashboard's filters. |
| You are asked to sign in again | Sign in again with your TERCEPT login. This happens after a period without use, or if your admin changed your access. |

## Support

For questions and problems, email [support@tercept.com](mailto:support@tercept.com).

**Useful links:** [TERCEPT](https://insights.tercept.com) · [Privacy policy](https://tercept.com/privacy-policy-2/)

*Last updated: 12 November 2026*
