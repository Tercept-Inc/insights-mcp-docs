# Tercept Insights MCP Server

Connect Claude, or any other AI assistant that supports MCP, to your Tercept Insights account. Ask questions about your
data, find dashboards and charts, run read-only SQL and manage scheduled reports, all in plain language.

| | |
|---|---|
| **Server URL** | https://insights-mcp.tercept.com/mcp |
| **Sign-in** | OAuth 2.0 with your Tercept Insights login |
| **Who can use it** | Tercept Insights users whose admin has turned on MCP access |
| **Support** | [gourav.chindlur@tercept.com] |

## Contents

1. [What is MCP?](#what-is-mcp)
2. [What the Tercept Insights MCP server does](#what-the-tercept-insights-mcp-server-does)
3. [How it works](#how-it-works)
4. [Before you start](#before-you-start)
5. [Connect your assistant](#connect-your-assistant)
6. [Tools](#tools)
7. [Example prompts](#example-prompts)
8. [Limits and logs](#limits-and-logs)
9. [Data and privacy](#data-and-privacy)
10. [Troubleshooting](#troubleshooting)
11. [Support](#support)

---

## What is MCP?

MCP (Model Context Protocol) is an open standard that lets AI assistants work with other applications. An application
publishes a set of tools through an MCP server, and the assistant calls those tools to look things up or take actions
on your behalf. You describe what you need, and the assistant decides which tools to call.

## What the Tercept Insights MCP server does

Tercept Insights is Tercept's analytics and reporting platform. Customers use it to bring together data from their ad
platforms, marketplaces and other sources, and to build reports and dashboards on top of it.

The Tercept Insights MCP server connects your Insights account to your AI assistant. Once connected, you can:

- Find dashboards, charts, data sources and saved queries, and ask what they show.
- Ask questions about your numbers. The assistant reads chart data, or writes and runs a read-only SQL query, to answer.
- Get a link to a new chart in Insights Explore, ready to adjust and save.
- Open a query in SQL Lab to continue working on it.
- Create, change or delete scheduled reports and alerts, and preview an alert email before you create it.
- Get help with Insights features and menus.

> **Example:** You ask Claude, "How did revenue by demand partner change last week compared with the week before?"
> Claude finds the right data source in your Insights account, checks its columns and metrics, runs a read-only query
> for both weeks and gives you the comparison along with the figures it used.

## How it works

1. You connect the server once and sign in with your Insights login.
2. When you ask a question, the assistant chooses the tools it needs, for example listing your data sources and then
   running a SQL query.
3. Each tool runs in Insights as you, using your Insights permissions, and returns the result to the assistant.
4. The assistant uses those results to answer you.

**Good to know**

- The assistant only knows what the tools return. The tools only list dashboards, charts and data sources that your
  Insights account can open.
- Clear questions get better answers. Naming the dashboard, data source, metric or date range you mean helps.
- If you don't give a date range for a large table, the assistant uses the data source's default window, or the last
  30 days.
- SQL access is read-only. Any query that would change data is refused.

## Before you start

You sign in on insights.tercept.com with the same login you use for Insights: username and password, or Google sign-in
if your company uses it. Your password is never shared with the assistant.

Your Insights admin controls who can use the server and what they can do:

| To do this | Your account needs |
|---|---|
| Connect | The **Can Access MCP** role, granted by your Insights admin |
| View dashboards, charts and data sources | Access to them in Insights |
| Run SQL queries | SQL Lab access in Insights |
| Create and manage scheduled reports and alerts | MCP access only |

Insights admins also have tools for creating and editing charts, dashboards and datasets. These tools are not shown to
other users.

## Connect your assistant

All users connect to the same server URL:

```
https://insights-mcp.tercept.com/mcp
```

The URL contains no key or password. Each user signs in separately with their own Insights login.

### Claude: from the Connectors Directory

1. In Claude, go to **Customize > Connectors** and search for **Tercept Insights**.
2. Click **Connect**. The Insights sign-in page opens.
3. Sign in. You are returned to Claude.
4. In a chat, open the **+** menu, go to **Connectors** and turn on **Tercept Insights**.

### Claude: as a custom connector

1. Go to **Customize > Connectors > Add custom connector**.
2. Enter **Tercept Insights** as the name and the server URL above.
3. Click **Add**, then **Connect**, and sign in.

### Claude Code

Run:

```
claude mcp add --transport http tercept-insights https://insights-mcp.tercept.com/mcp
```

Then type /mcp in Claude Code, select **tercept-insights** and choose **Authenticate**. The Insights sign-in page opens
in your browser.

### Other assistants

Any MCP client that supports remote servers over HTTP with OAuth sign-in can connect using the same URL.

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
| Help and account | get_platform_help | Answers questions about Insights features and menus |
| | get_mcp_usage | Shows how much of your daily data limit you have used |
| | get_schema | Lists the fields you can filter and sort on |
| | health_check | Checks that the server is running |
| Other | list_tags, get_tag_info | Tags and their details |
| | list_annotation_layers, get_annotation_layer_info, list_layer_annotations, get_layer_annotation_info | Annotation layers and annotations |
| | list_roles, get_role_info, list_users, get_user_info | Roles and users (some details are visible to admins only) |

### Tools that make changes

| Tool | What it does |
|---|---|
| generate_explore_link | Creates a link to a new chart in Explore. Nothing is saved until you save it in Insights |
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

## Limits and logs

| | |
|---|---|
| **Rate limits** | Each user can call each tool a limited number of times per minute. If you reach the limit, wait a minute and try again. |
| **Daily data limit** | SQL queries on ClickHouse data sources count towards a daily limit on the amount of data scanned: 200 GB by default, unless your admin has set a different limit. Ask the assistant how much you have used. |
| **Logs** | Tercept logs each tool call (user, tool, time and outcome) and, for SQL queries, a short preview of the query and the amount of data it read. These logs are used for security, support and the limits above. |

## Data and privacy

- **What the assistant receives:** the results of the tools it calls, such as chart data, query results and the names
  and descriptions of your Insights objects. These become part of your conversation and are governed by your AI
  provider's terms and your settings with that provider.
- **What Tercept stores:** the logs described above, kept for [retention period]. Your sign-in stays active for up to
  30 days and renews while you use the server.
- **What Tercept does not do:** [legal to confirm, for example: we do not sell this data or share it with third parties].
- **More information:** see the [Tercept privacy policy](https://tercept.com/privacy-policy-2/).

**Disconnecting:** remove the connector in your assistant (in Claude, **Customize > Connectors**). Your Insights admin
can also remove your MCP access, which stops all tool calls immediately.

## Troubleshooting

| Problem | Solution |
|---|---|
| "Couldn't reach the MCP server" or "Authorization failed" when connecting | Check that the URL is exactly https://insights-mcp.tercept.com/mcp and try again. If the problem continues, contact support and include the time it happened. |
| A message saying your account does not have MCP access | Ask your Insights admin for the **Can Access MCP** role. |
| A SQL query is refused | Only read-only queries are allowed. You may also need SQL Lab access, which your admin can grant. |
| A rate limit or daily data limit message | Wait and try again, or narrow the question with a shorter date range or fewer columns. |
| The answer does not match a dashboard | Dashboards often apply filters. Name the chart and ask the assistant to use that chart's data, or check the dashboard's filters. |
| You are asked to sign in again | Sign-ins last up to 30 days and renew while you use the server. Sign in again after a long break or if your admin changed your access. |

## Support

| | |
|---|---|
| **Questions and problems** | [gourav.chindlur@tercept.com] |

**Useful links:** [Tercept Insights](https://insights.tercept.com) · [Privacy policy](https://tercept.com/privacy-policy-2/) ·
[Model Context Protocol](https://modelcontextprotocol.io)

*Last updated: [publish date]*
