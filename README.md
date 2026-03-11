<div align="center">

# Google Analytics 4 MCP Server by Coupler.io

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Transport](https://img.shields.io/badge/Transport-Streamable_HTTP-blue.svg)](#)
[![Auth](https://img.shields.io/badge/Auth-OAuth_2.0-green.svg)](#)

Coupler.io Google Analytics 4 (GA4) MCP server for Claude, ChatGPT, Gemini, Cursor, n8n, OpenClaw, and other MCP clients. Query and analyze Google Analytics data with natural language. Requires the Coupler.io account.

</div>

## Data Access

Access a flexible, customizable report type with your choice of metrics (page views, sessions, users, revenue) and dimensions (date, country, traffic source, page path) from your GA4 properties.

<details>
<summary><strong>Available metrics</strong></summary>

#### Traffic & Engagement

| Metric | Description |
|---|---|
| **Views** | Total page views (or screen views for apps) |
| **Sessions** | Number of sessions started |
| **Total users** | Total number of unique users |
| **New users** | Users who visited for the first time |
| **Active users** | Users who had an engaged session |
| **Bounce rate** | Percentage of sessions that were not engaged |
| **Engagement rate** | Percentage of sessions that were engaged (inverse of bounce rate) |
| **Average session duration** | Average length of a session in seconds |
| **Views per session** | Average number of pages viewed per session |
| **Sessions per user** | Average number of sessions per user |
| **Event count** | Total number of events triggered |
| **Key events** | Total number of key events (formerly conversions) |

#### E-commerce

| Metric | Description |
|---|---|
| **Purchase revenue** | Total revenue from purchases |
| **Total revenue** | Total revenue including purchases, subscriptions, and ad revenue |
| **Ecommerce purchases** | Number of completed purchases |
| **Add-to-carts** | Number of add-to-cart events |
| **Checkouts** | Number of checkout events |
| **Item revenue** | Revenue from individual items |
| **Transactions** | Number of transactions |
| **Average purchase revenue** | Average revenue per purchase |

#### Advertising

| Metric | Description |
|---|---|
| **Ads cost** | Cost of linked advertising campaigns |
| **Ads clicks** | Clicks from linked ad campaigns |
| **Ads impressions** | Impressions from linked ad campaigns |
| **Return on ad spend** | Revenue generated per unit of ad spend |
| **Cost per key event** | Ad cost per key event |

</details>

<details>
<summary><strong>Available dimensions</strong></summary>

#### Time

| Dimension | What it shows |
|---|---|
| **Date** | Daily breakdown (YYYYMMDD) |
| **Date + hour** | Hourly breakdown |
| **Day of week** | Which day of the week (0 = Sunday) |
| **Month, Week, Year** | Broader time periods |

#### Traffic Source

| Dimension | What it shows |
|---|---|
| **Session source** | Where the session originated (e.g., google, facebook) |
| **Session medium** | The marketing medium (e.g., organic, cpc, referral) |
| **Session source / medium** | Combined source and medium |
| **Session campaign** | The campaign name from UTM parameters |
| **Default channel group** | Google's auto-classified channel (Organic Search, Paid Search, etc.) |

#### Geography & Technology

| Dimension | What it shows |
|---|---|
| **Country, City, Region** | User location |
| **Device category** | Desktop, mobile, or tablet |
| **Browser** | User's browser (Chrome, Safari, etc.) |
| **Operating system** | User's OS (Windows, iOS, Android, etc.) |

#### Content

| Dimension | What it shows |
|---|---|
| **Page path** | The URL path of the page viewed |
| **Page title** | The title of the page viewed |
| **Landing page** | The first page of the session |
| **Hostname** | The domain name |

#### E-commerce

| Dimension | What it shows |
|---|---|
| **Item name, Item ID** | Product identifiers |
| **Item category** (1–5) | Product category hierarchy |
| **Item brand** | Product brand |
| **Transaction ID** | Unique transaction identifier |

</details>


## Supported Clients

*Note: You will need to set up a data flow in Coupler.io with Google Analytics 4 as a source and the AI tool of your choice as the destination.*

### Claude

Use with Claude Web, Desktop, Chat, Cowork, or Claude Code.

**Via Web/Desktop:** Go to **Customize**->**Connectors**->**Connect your tools**, search for Coupler.io and add it.

**Via Claude Code CLI:**

```bash
claude mcp add coupler-io --transport streamable-http https://mcp.coupler.io/mcp
```

### ChatGPT

Install from the **ChatGPT Apps** directory — search for "Coupler.io" in the **Apps** section of **Settings**.

### Cursor

Find it on the [Cursor Directory](https://cursor.directory/mcp/coupler-io-official-remote-mcp).

### Gemini CLI

Go to the **AI integrations** -> **Gemini CLI** page in your Coupler.io account to copy the correct command (unique to each account). It will look like this:

```bash
gemini mcp add coupler --transport=http https://mcp.coupler.io/mcp/xxxxx
```

### OpenClaw

Use the **mcporter** skill to connect, or install the **coupler-io** skill from ClawHub.
Directly ask your OpenClaw agent to add the skill and execute it.

## Links

- **Landing page:** [Google Analytics 4 MCP by Coupler.io](https://www.coupler.io/mcp/google-analytics)
- **Coupler.io:** [https://coupler.io](https://coupler.io)
- **MCP Server endpoint:** `https://mcp.coupler.io/mcp`