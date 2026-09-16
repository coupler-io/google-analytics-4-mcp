<div align="center">

# Google Analytics 4 MCP Server by Coupler.io

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Transport](https://img.shields.io/badge/Transport-Streamable_HTTP-blue.svg)](#)
[![Auth](https://img.shields.io/badge/Auth-OAuth_2.0-green.svg)](#)

Connect Google Analytics 4 (GA4) data to AI with the Coupler.io MCP server. Ask natural-language questions about website traffic, user acquisition, engagement, landing pages, conversions, ecommerce revenue, and advertising performance in ChatGPT, Claude, Gemini, Cursor, and other MCP-compatible AI tools. Requires a Coupler.io account.

[Landing page](https://www.coupler.io/mcp/google-analytics) · [Documentation](https://docs.coupler.io/ai/mcp) · [All Coupler.io MCP integrations](https://github.com/coupler-io)

</div>

## What you can ask

- Which traffic channels generated the most conversions last month?
- Which landing pages have the highest engagement rate?
- Why did ecommerce revenue decline this week?
- Compare mobile and desktop conversion performance.
- Which sources bring the highest-value users?

## How it works

This repository documents the Google Analytics 4 integration for the Coupler.io MCP server.

1. Connect Google Analytics 4 to Coupler.io.
2. Select your AI tool as the destination.
3. Connect your AI client to Coupler.io MCP.
4. Ask questions about your Google Analytics 4 data in natural language.

Coupler.io sits between Google Analytics 4 and your AI client. It holds the Google Analytics 4 credential, imports the data on a schedule, and exposes the result as a data set the AI can query. Your AI client never calls the Google Analytics 4 API itself.

```
  Google Analytics 4
      |        credential held by Coupler.io
      v
  Coupler.io          import, transform, store on a schedule
      |
      v
  MCP server          schema, SQL query execution
      |
      v
  Your AI client      your question, in plain language
```

When you ask a question, the AI reads the data set's schema, writes SQL, and Coupler.io runs that query on its own side. Only the result comes back to the AI, so a large data set does not have to fit into the model's context window.

| | |
|---|---|
| **MCP endpoint** | `https://mcp.coupler.io/mcp` |
| **Transport** | Streamable HTTP |
| **Authentication** | OAuth 2.0 |
| **Query language** | SQL, executed by Coupler.io |
| **Refresh schedule** | From monthly to every 15 minutes, depending on your plan |

## Get started

*Note: You will need to set up a data flow in Coupler.io with Google Analytics 4 as a source and the AI tool of your choice as the destination.*

### Claude

Use with Claude Web, Desktop, Chat, Cowork, or Claude Code.

**Via Web/Desktop:** Go to **Customize**->**Connectors**->**Connect your tools**, search for Coupler.io and add it.

**Via Claude Code CLI:**

```bash
claude mcp add coupler-io --transport streamable-http https://mcp.coupler.io/mcp
```

### ChatGPT

Install the [Coupler.io ChatGPT app](https://l.rw.rw/couplerio-chatgpt-app) and complete the authentication. You can also find it by searching for "Coupler.io" in the **Apps** section of **Settings**.

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

## Data you can access

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

You configure a GA4 source by choosing metrics and dimensions. Coupler.io imports only the ones you select, and GA4's own compatibility rules limit which combinations you can request together.

## Example questions

### Acquisition

- Which default channel groups generated the most key events last month?
- Which session sources bring users with the highest engagement rate?
- Compare paid search and organic search sessions and conversions month over month.

### Content and behavior

- Which landing pages have the highest engagement rate and the most sessions?
- Which pages have a high bounce rate but significant traffic?
- Compare conversion performance across desktop, mobile, and tablet.

### Ecommerce

- Why did purchase revenue decline this week compared with last week?
- Which item categories contributed most to revenue growth?
- What is the drop-off between add-to-carts, checkouts, and purchases?

## Security and permissions

Your AI client never connects to Google Analytics 4 directly. Coupler.io holds the Google Analytics 4 credential, imports the data, and exposes only the resulting data set over MCP.

- **Your Google Analytics 4 data is never modified.** Coupler.io only reads from Google Analytics 4. The AI queries the copy Coupler.io imported and cannot edit, delete, or overwrite it, let alone write anything back to your Google Analytics 4 account.
- **Visibility is scoped per AI tool.** An AI client sees only the data sets from data flows that have *that client* set as a destination. Adding Claude as a destination does not expose the data flow to ChatGPT, though one flow can name both.
- **Configuration changes are possible, and confirmed first.** With the full tool set available, the AI can create data flows, add sources and destinations, change a schedule, or trigger a run. Those are real changes to your workspace, so the server instructs the AI to confirm before making one you did not ask for.
- **Nothing else is reachable.** The MCP server exposes the data sets described above and nothing more. It cannot reach your other accounts or your machine.
- **Disconnect at any time** by removing the connector in your AI client, or by deleting the credential or the data flow in Coupler.io.

Coupler.io is SOC 2 certified and compliant with GDPR and HIPAA.

## Troubleshooting

**The AI cannot find my Google Analytics 4 data set.**
Usually you have not added that AI tool as a destination yet. Open the data flow in Coupler.io and add your AI client. One data flow can have several AI tools as destinations at the same time, so adding ChatGPT does not displace Claude. Each tool sees only the flows it is named on.

**The numbers look out of date.**
The AI reads the last imported snapshot, not Google Analytics 4 live. Check the data flow's refresh schedule, or ask your AI client to run the data flow now.

**A field I need is missing.**
Coupler.io imports only the metrics and dimensions you select in the data flow's source. Add the ones you need and re-run the flow, within GA4's compatibility rules.

**The AI misreads a metric.**
Save the business context on the data set: what a metric means, which currency it is in, which rows to exclude. You do not have to leave your AI tool to do it, just tell the assistant to update the data set context and it saves it for you. The AI reads that context before it queries, so the next conversation uses your definitions instead of guessing.

**The connector does not appear in my AI client.**
Availability differs by AI client and subscription plan. Follow the client-specific steps under [Get started](#get-started), and check the [AI destination docs](https://docs.coupler.io/destinations/categories/ai) for that tool.

## Related Coupler.io MCP integrations

- [Google Ads MCP](https://github.com/coupler-io/google-ads-mcp) — connect paid search performance with website behavior and conversions
- [Facebook Ads MCP](https://github.com/coupler-io/facebook-ads-mcp) — analyze paid social traffic and conversion performance
- [Shopify MCP](https://github.com/coupler-io/shopify-mcp) — combine website analytics with ecommerce orders and product data
- [Google BigQuery MCP](https://github.com/coupler-io/google-bigquery-mcp) — analyze GA4 and other business data stored in BigQuery

[Explore all Coupler.io MCP integrations](https://github.com/coupler-io)

## FAQ

### What is the Google Analytics 4 MCP server?

It is the Google Analytics 4 integration for the Coupler.io MCP server, an endpoint that lets AI clients query your Google Analytics 4 data in plain language. Coupler.io imports the data, stores it, and answers the AI's SQL queries on its own infrastructure.

### Do I need a Coupler.io account?

Yes. The MCP server serves data from your Coupler.io workspace, so you need an account with a data flow that has Google Analytics 4 as a source and your AI tool as a destination.

### Does this connect directly to my Google Analytics 4 account?

No. Coupler.io connects to Google Analytics 4, imports the data, and exposes the resulting data set over MCP. Your AI client talks to Coupler.io, never to Google Analytics 4.

### Which Google Analytics 4 data can AI access?

Whatever your data flow imports. See [Data you can access](#data-you-can-access) for the full catalog of report types and fields. The AI reaches only the data sets in flows that name your AI tool as a destination.

### Is the integration read-only?

Yes. Nothing you or your AI client does through Coupler.io changes your Google Analytics 4 data. Coupler.io only reads from Google Analytics 4, and the AI only queries the copy Coupler.io imported. It cannot edit, delete, or write anything back to your Google Analytics 4 account.

### Which AI assistants can I use?

Claude, ChatGPT, Cursor, Gemini CLI, OpenClaw, Perplexity, and any client that speaks MCP through the Custom MCP destination. Setup steps for the clients above are under [Get started](#get-started); for the rest, see the [AI destination docs](https://docs.coupler.io/destinations/categories/ai).

### Do I need to write SQL or code?

No. You ask in plain language; the AI writes the SQL and Coupler.io runs it. Writing SQL yourself stays an option if you want a specific transformation.

### How fresh is the data?

As fresh as the last data flow run. Schedules range from monthly to every 15 minutes depending on your plan, and you can ask your AI client to refresh the flow on demand.

## Links

- **Landing page:** [Google Analytics 4 MCP by Coupler.io](https://www.coupler.io/mcp/google-analytics)
- **Documentation:** [Coupler.io MCP](https://docs.coupler.io/ai/mcp)
- **Coupler.io:** [https://coupler.io](https://coupler.io)
- **MCP Server endpoint:** `https://mcp.coupler.io/mcp`
- **All Coupler.io MCP integrations:** [https://github.com/coupler-io](https://github.com/coupler-io)
