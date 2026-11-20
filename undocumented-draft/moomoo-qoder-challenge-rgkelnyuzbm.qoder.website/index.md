---
kgWebpageUrl: "https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/"
kgWebpageView: "markdown"
---

# 2026 Moomoo x Qoder AI Trading Agent Challenge

![Moomoo](data:,)

×

![Qoder](data:,)

Participant Handbook Event Details Moomoo Paper Trading Account Terms & Conditions Terms & Conditions FAQ Disclaimer

On this page

- [1. Qoder account and subscription](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/#hb-part-1)

- [2. Trade in the competition paper trading account](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/#hb-part-competition)

- [3. Install and Set up Qoder Desktop](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/#hb-part-2)

- [3.1 Add the Moomoo MCP connector](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/#hb-part-2-mcp)
- [3.2 Add the official Moomoo skill](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/#hb-part-2-skill)
- [3.3 Add the Qoder Cloud Agents Plugin](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/#hb-part-2-plugin)

- [4. Set up Moomoo MCP and Skills in Qoder Cloud Agents](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/#hb-part-3)

- [4.1 Moomoo MCP in Vault](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/#hb-part-3-vault)

- [4.2 Moomoo Skills in Qoder Cloud Agents](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/#hb-part-3-skills)

- [4.2.1 Package the skills for Cloud Agents](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/#hb-part-4-package)
- [4.2.2 Upload in the console](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/#hb-part-4-upload)

- [5. Channel configuration (Slack)](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/#hb-part-5)

- [5.1 Where the channel settings live](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/#hb-part-5-where)
- [5.2 Create the Slack app](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/#hb-part-5-bot)
- [5.3 Connect the app to Qoder](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/#hb-part-5-connect)
- [5.4 Send the first message](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/#hb-part-5-test)

- [6. Schedule automated runs (Forward Mode)](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/#hb-schedule)

- [6.1 Describe a good scheduled task](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/#hb-schedule-1)
- [6.2 Ready-to-copy examples](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/#hb-schedule-2)
- [6.3 Choose a time zone](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/#hb-schedule-3)
- [6.4 API configuration examples](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/#hb-schedule-4)
- [6.5 Manage tasks and view results](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/#hb-schedule-5)
- [6.6 Tips for using Schedule effectively](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/#hb-schedule-6)

- [7. Create a dashboard](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/#hb-part-6)

- [8. Tips and tricks: fine-tuning agents](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/#hb-part-7)

- [8.1 Keep a local copy and version history of your agents](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/#hb-part-7-version)
- [8.2 Tuning the agent](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/#hb-part-7-agent)

- [9. Let agents collaborate (Forward Mode)](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/#hb-part-8)

## Participant Handbook

[Qoder Deck ](https://ngynckpj.qwenwork.page/) [Moomoo Deck ](https://moomoo-strategy-briefing-j692pppjg7l.qoder.website/#s=1) [Zoom Recording](https://drive.google.com/file/d/1e0s5JcAhRr6TaHqrzfXBHQb8FZBbnbMq/view)

## 1. Qoder account and subscription

1. Go to [https://qoder.com/users/sign-up](https://qoder.com/users/sign-up) and create an account.
2. **Use the same email address as your [Luma registration](https://luma.com/oezyv35j).** The Pro Plan will be attached to that address; an account created with a different email will not receive it.

![Qoder Sign Up page](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/images/01-signup-qoder.png)

Qoder Sign Up page
3. Sign in to Qoder and open [**Settings → My Billing**](https://qoder.com/account/plan) to confirm you are on **Pro**.

![My Billing page with the Pro plan highlighted in red](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/images/03-pro-plan.png)

My Billing page
4. If you do not see the Pro Plan, contact the organisers with your Qoder email and your Luma name.

## 2. Trade in the competition paper trading account

**All trades must be placed in the dedicated competition paper trading account.** Trades made in any other paper trading account do not count toward your challenge ranking.

1. In the moomoo app, open **Discover → Paper Trade → Competition**.
2. Under **Ongoing**, find **Moomoo x Qoder AI Paper Trading Agent Challenge** and select it.

![Moomoo Paper Trade Competition tab showing the Moomoo x Qoder AI Paper Trading Agent Challenge account with USD 100,000 in net assets](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/images/15-competition-paper-account.png)

Competition → Ongoing — Moomoo x Qoder AI Paper Trading Agent Challenge
3. Confirm the account is active: the Paper Trade screen shows the competition account name at the top, and **Net Assets** displays your competition balance.
4. If you have more than one paper trading account, always double-check the account name before placing trades — your agent must trade in this account only.

## 3. Install and Set up Qoder Desktop

1. Download the Desktop app from [qoder.com/download](https://qoder.com/download).
2. Launch Qoder and sign in with the account you created in step 1.
3. **Optional but recommended:** create a project folder for the hackathon (for example `moomoo-trading-agent`) and open it in Qoder as your workspace. Keeping everything you generate — skills, code, dashboards, decision logs — in one folder makes packaging your submission much easier.

### 3.1 Add the Moomoo MCP connector

The connector adds the Moomoo MCP server to Qoder Desktop in one step.

1. In the left sidebar, open **Extensions → Connectors**.
2. Search for **moomoo**. The official connector is **moomoo Open API**, published by *moomoo*.
3. Click **View details** to review the publisher and requested permissions, then **Install**.

![moomoo Open API connector detail page in Qoder Desktop, published by Moomoo, showing the hosted moomoo MCP server with HTTP transport, OAuth authentication and the endpoint https://mcp.moomoo.com/mcp, with an Install button](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/images/02-moomoo-openapi-connector.png)

Connectors → moomoo Open API: publisher, MCP server details and Install
4. When the browser opens, sign in with your **Moomoo ID** and complete the OAuth authorisation.
5. Enable the connector for the session: open the MCP/tools selector in the chat prompt and switch on **moomoo**.
Then verify it with a read-only request such as `What is the current price of US.AAPL?` Make sure a quote comes back before you try anything that touches an account.

### 3.2 Add the official Moomoo skill

The connector provides the MCP server; the official **moomoo-skill** (published by *moomoo*) adds the skills for this event: quotes, news, sentiment, unusual activity, simulated trading, and the grid strategy.

1. In Qoder Desktop, go to **Extensions → Skills** and search for **moomoo**.

![Qoder Desktop Skills marketplace with moomoo searched, showing the moomoo-skill entry marked Partner under New and noteworthy and All skills](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/images/04-moomoo-skill-search.png)

Extensions → Skills: search for moomoo to find the official skill
2. Click into **moomoo-skill** and confirm the publisher is *moomoo*.
3. Under *One-click install to client*, click **Install** and choose **Qoder**. The next new Qoder session will pick up the skill automatically.
4. To use the skill, mention it by name in your request (for example, "use the moomoo-skill to check …") and Qoder loads it on demand. Verify with a read-only request such as `What is the current price of US.AAPL?`

### 3.3 Add the Qoder Cloud Agents Plugin

The official **Qoder Cloud Agents** plugin (published by *Qoder*) bundles everything you need to drive the cloud side from Qoder Desktop: the managed **qca MCP connector** and the **qoder-cloud-agents** skill. Together they let you manage agents, environments, sessions, files, vault credentials and deployments directly from chat.

1. In Qoder Desktop, open **Extensions → Plugins** and search for **Qoder Cloud Agents**.
2. Confirm the publisher is *Qoder* (marked **Recommend**), then click **Install** — or use *One-click install to client* from the Marketplace detail page.
3. Restart or reload Qoder. The `qca` connector and `qoder-cloud-agents` skill are picked up automatically in a new session.

**🎉 That's it — Qoder Desktop is set up.**

## 4. Set up Moomoo MCP and Skills in Qoder Cloud Agents

Cloud Agents run in their own container, with no browser session and no local Open D, so they cannot reuse your Desktop login. Authentication goes through a **Vault** instead.

### 4.1 Moomoo MCP in Vault

A **Vault** stores the Moomoo OAuth credential that cloud sessions use. The token is kept in the vault and refreshed automatically; it is never displayed after authorisation, so there is nothing to copy.

1. Open the [Cloud Agents console](https://qoder.com/cloud-agents) and select **Forward Mode** in the sidebar.
2. Open **Vault** and click **Create** to add a new vault (for example, `moomoo-mcp`).
3. In the new vault, click **Add** and add Moomoo as a **custom MCP**: choose **MCP OAuth** as the credential type, enter `https://mcp.moomoo.com/mcp` as the MCP Server URL, leave **Access Token** and the **OAuth client credentials** empty, then click **Connect**.

![Vault Add dialog with Credential Type set to MCP OAuth and MCP Server set to https://mcp.moomoo.com/mcp, Access Token and OAuth client credentials left empty](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/images/11-vault-add-mcp.png)

Vault → Add: an MCP OAuth credential for the custom Moomoo MCP server
4. The Moomoo OAuth screen opens. Sign in with your **Moomoo ID**, select the account to authorise, approve the requested permissions (Market Data and Watchlists are selected by default), tick the licence-agreement box, and click **Confirm**.

![moomoo Open API OAuth consent screen listing Market Data, Watchlists, Accounts & Orders and Trade Execution permissions, with the licence-agreement checkbox and Confirm button](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/images/12-moomoo-oauth.png)

Moomoo OAuth consent — approve the permissions and Confirm

Once connected, the vault holds a valid `mcp_oauth` credential for the Moomoo MCP server. Attach this vault to every agent or session that needs Moomoo tools; a session without the vault will simply have no Moomoo tools and will not warn you.

### 4.2 Moomoo Skills in Qoder Cloud Agents

Cloud sessions do not inherit your Desktop skills. Giving a Cloud Agent the Moomoo skills takes two steps: package each skill as a Cloud Agents–compatible archive, then upload it in the Cloud Agents console.

#### 4.2.1 Package the skills for Cloud Agents

Desktop skill folders and Cloud Agents skill archives have different structures. Package **one zip per skill** — do not combine several skills into a single archive. Each zip must contain exactly one top-level folder named after the skill's `name` in `SKILL.md`, holding `SKILL.md` plus its references, scripts and assets. Keep each zip under 50 MB, make sure the frontmatter carries `name` and `description`, and include any shared reference files the skill links to, repairing relative links in the packaged copies.

The fastest way is to ask Qoder Desktop to do the packaging for you. Paste this prompt:

TEXTCopy

> Package the skills from [github.com](https://github.com/MoomooOpen/moomoo-agent-hub/blob/main/docs/moomoo-install.md) into ZIP files compatible with Qoder Cloud Agents, ready for manual upload.
>
> Requirements:
>
> - Create ONE ZIP PER SKILL. Do not combine skills or create an all-in-one wrapper.
> - Follow QCA's official package rules: [https://docs.qoder.com/cloud-agents/api/skills/schemas.md](https://docs.qoder.com/cloud-agents/api/skills/schemas.md)
> - Each ZIP must contain exactly one top-level folder matching the YAML `name` in its SKILL.md:
>   ```
>   skill-name.zip
>   └── skill-name/
>       ├── SKILL.md
>       └── references, scripts, assets, etc.
>   ```
> - Include all required supporting files, including shared references outside the original skill folder. Repair relative links in the packaged copies where needed.
> - Preserve the skill instructions and safety rules. Leave the originals unchanged.
> - Exclude credentials, tokens, .git, .DS_Store, __MACOSX, and unrelated files.
> - Validate ZIP integrity, folder/name matching, YAML frontmatter, required name/description fields, size limits, and local reference links.
> - If anything cannot be validated or a required file is missing, report it rather than claiming the package is ready.
> - Do not install dependencies, run the skills, upload anything, or modify my installed skills.
>
> Return links to the ZIPs and a brief validation summary. Distinguish local format validation from actual QCA upload acceptance.

Qoder returns one zip per skill plus a validation summary. Treat that as a local format check only; the upload in the next step is where Cloud Agents actually accepts or rejects each package.

#### 4.2.2 Upload in the console

Upload the zips manually in the Cloud Agents console:

1. Open the [Cloud Agents console](https://qoder.com/cloud-agents), then **Skills** in the sidebar.
2. Click **Create Skill**, then drag a packaged skill zip into the dialog — or click the drop area to browse. Only `.zip` files are accepted (max 50 MB), and each package must contain a `SKILL.md` with a name and description. Repeat for each skill zip — one upload per skill.

![Create Skill dialog with a drag-and-drop area for .zip skill packages and a Create Skill button](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/images/13-cloud-create-skill.png)

Skills → Create Skill: drop the skill zip in, or click to browse

![Skill Center list showing the uploaded moomoo skills, each marked Custom with a version number](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/images/14-cloud-skill-center.png)

Skill Center with the uploaded Moomoo skills

## 5. Channel configuration (Slack)

Cloud Agents can route a Template/Identity conversation to a delivery channel, so your agent can post its outputs (pre-market scan, risk alerts, trade-log summary) into a chat rather than only into a session. This is what counts towards the "automation" half of the usage score.

### 5.1 Where the channel settings live

Channels belong to a Template — there is no standalone "Channels" page. Open the Cloud Agents console at [qoder.com/cloud](https://qoder.com/cloud), select **Forward Mode** in the sidebar, then **Templates**.

![Forward Mode Templates page with the Templates item selected in the sidebar and the My Templates list](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/images/06-cloud-templates.png)

Forward Mode → Templates

1. Open the template your agent runs on, or create one with **Create Template → Custom Create**. A name, a model, and the **Default** environment are enough to start.
2. In the template editor, open the **Channels** tab (between *Collaboration* and *Integration*). It shows one card per messaging provider — DingTalk, Feishu, Lark, WeCom, WeChat, Slack and Microsoft Teams — and each card can hold up to five console-created bots.
3. Scroll to the **Slack** card and click **Create Bot**.

![Channels tab of a template showing the Slack card with a Create Bot button](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/images/07-cloud-channels-tab.png)

Channels tab → Slack → Create Bot

### 5.2 Create the Slack app

In Qoder's **Create Bot** dialog, click **Go to channel admin console**. This opens Slack Apps at [https://api.slack.com/apps](https://api.slack.com/apps). Keep the Qoder dialog open so you can return with your tokens.

![Qoder Create Bot dialog with the Go to channel admin console link above the empty App Token and Bot Token fields](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/images/08-slack-create-bot.png)

Qoder → Create Bot → Go to channel admin console

In Slack, click **Create New App** and follow the prompts to name your app and select your Slack workspace. Your workspace may require administrator approval.

![Slack Your Apps page with the Create New App button; existing app details are obscured](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/images/17-slack-apps.png)

Slack Apps → Create New App

Once you create the app, you should see your app details. Copy the **App token** beginning with `xapp-` and the **Bot token** beginning with `xoxb-` to enter in Qoder.

![Slack app created and installed confirmation showing masked Bot token, User token and App token fields](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/images/18-slack-app-credentials.png)

Copy the Bot token and App token; the User token is not needed

### 5.3 Connect the app to Qoder

Return to Qoder's **Create Bot** dialog and fill in:

- **Name** — a recognisable label, e.g. `moomoo-trader-alerts`.
- **Channel mode** — **Open mode** lets anyone chat with the bot without approval; **Pairing mode** requires a new chat to be paired before it can use your agent. The mode cannot be changed after creation. Choose Pairing mode if the workspace includes people who should not be able to give your agent tasks.
- **App Token** — paste the Slack App token beginning with `xapp-`.
- **Bot Token** — paste the Slack Bot token beginning with `xoxb-`. The User token beginning with `xoxp-` is not needed.
- **Show Thinking** / **Show Tool Calls** — leave both off unless you want those details mirrored into Slack.

Click **Save**. The Slack card should then show the bot as **Console 1/5**.

**Keep both tokens private.** Enter them only in the token fields, never in prompts, source code, dashboards, reports or unmasked screenshots.

### 5.4 Send the first message

Invite the app to your Slack channel and mention it, or message it directly. Start with a harmless connection check:

`@YourBot Say hello and confirm you can reply. Do not place any trades.`

In Pairing mode, complete pairing when prompted, then resend your message. If there is no reply, check Socket Mode, event subscriptions, workspace installation and channel membership.

Slack setup reference: [https://docs.slack.dev/tools/bolt-python/creating-an-app](https://docs.slack.dev/tools/bolt-python/creating-an-app).

## 6. Schedule automated runs (Forward Mode)

Schedule lets your assistant run a task automatically at a set time — check a status every five minutes, generate a daily briefing, or send a one-off reminder. Once a schedule is created, you do not need to keep the conversation that created it online. You can create one in natural language in a Forward Mode conversation, or configure it precisely through the API.

### 6.1 Describe a good scheduled task

Include four things in a single request: **what to run**, **when to run it**, **which time zone** to use, and **how to output the results**. For monitoring tasks, also specify the start and end times. This template works well:

```
Please create a scheduled task named "Task Name".
Execution time: Frequency or specific date and time.
Time zone: An explicit time zone, such as Asia/Shanghai.
Task details: Data sources, items to check, and specific objectives.
Output requirements: Format, number of items, filtering criteria, etc.
For temporary monitoring: Specify the start date and time and the end date and time.
After creation, please confirm the task ID, scheduling rule, time zone, and next scheduled execution time.
```

Before using Schedule, confirm that the agent's template has the **Schedule capability** enabled. If you do not have permission to configure it, contact your administrator. The data access permissions, tools and credentials the task needs must also be configured in advance.

### 6.2 Ready-to-copy examples

The data source names below are examples. Replace them with systems, files or projects that your assistant can actually access.

#### Example A: run every five minutes

```
Please create a scheduled task named "Order Sync Check".
Starting after the task is successfully created, check the order synchronization system for failure records every 5 minutes.
Use the Asia/Shanghai time zone, with no end time.
For each run, summarize the number of failures, failure reasons, and related order IDs from the 5 minutes preceding the current check time.
If there are no failure records, briefly output "No failure records found in this check."
After creation, please confirm the task ID, execution interval, and next scheduled execution time.
```

If you want execution aligned to five-minute clock boundaries, such as 09:00, 09:05, 09:10, say so explicitly:

```
Please run the order sync check at minutes 00, 05, 10, 15, 20, 25, 30, 35, 40, 45, 50, and 55 of every hour in the Asia/Shanghai time zone.
Please use the cron rule */5 * * * *.
```

The difference is that a fixed interval is measured from the creation time, while five-minute clock boundaries align with the clock. If the task is created at 09:02, the first execution is scheduled for approximately 09:07 with the former and 09:05 with the latter. The scheduled trigger time may also differ from the actual start and completion times.

#### Example B: every day at 9:00 AM Beijing time

```
Please create a scheduled task named "Daily Industry Briefing".
Run it every day at 9:00 AM Beijing time, using the Asia/Shanghai time zone.
Summarize AI industry news from the past 24 hours using the configured news sources.
Select the 5 most important stories, each with a title, a one-sentence summary, and a source link.
After creation, please confirm the scheduling rule, time zone, and next scheduled execution time.
```

#### Example C: Monday through Friday at 9:00 AM New York local time

```
Please create a scheduled task named "US East Coast Team Morning Briefing".
Run it Monday through Friday at 9:00 AM New York local time, using the America/New_York time zone.
Summarize outstanding high-priority items, blockers, and tasks due today from the project management system.
Output a Markdown table with the columns "Item / Owner / Due Date and Time / Risk".
Schedule it according to New York local time, maintaining 9:00 AM local execution after daylight saving time changes.
```

Here, "Monday through Friday" refers only to the day of the week; it does not automatically exclude local public holidays.

#### Example D: every Monday at 10:00 AM Los Angeles local time

```
Please create a scheduled task named "Weekly Project Review".
Run it every Monday at 10:00 AM Los Angeles local time, using the America/Los_Angeles time zone.
Using records from the previous Monday through Sunday in the project management system, summarize completed items, unresolved risks, and this week's to-dos.
Use Markdown, with no more than 5 items per section, and include the corresponding task links.
```

#### Example E: check every five minutes within a set time window

```
Please create a scheduled task named "Release Window Health Check".
Run it only between 09:00 and 18:00 Beijing time on May 1, 2027, using the Asia/Shanghai time zone.
Starting at 09:00, check service error rates and availability in the configured monitoring system every 5 minutes.
For each run, list abnormal metrics and their monitoring links; if there are no abnormalities, briefly output the check results.
Do not trigger any new checks from 18:00 onward.
After creation, please confirm the start time, end time, and next scheduled execution time.
```

This window includes 09:00 but excludes 18:00, so the last scheduled trigger is at 17:55. The end time prevents new triggers; it does not immediately terminate executions that have already started.

#### Example F: run once at a set time, or after a delay

```
Please run once at 3:00 PM Beijing time on May 1, 2027, using the Asia/Shanghai time zone.
Remind me to prepare for the project review and list the materials to prepare in advance: a presentation, a progress summary, and a risk list.
```

```
Please run once in 30 minutes to check the release approval status in the project management system.
Tell me which approvals are still outstanding and include the approval links.
```

When specifying a date, choose a future time and include the year to avoid ambiguity in expressions such as "next Friday" or "3:00 PM".

### 6.3 Choose a time zone

Use an explicit IANA time zone name:

-\| Business time\| Time zone value\|
-\| Beijing time\| Asia/Shanghai\|
-\| Singapore time\| Asia/Singapore\|
-\| Tokyo time\| Asia/Tokyo\|
-\| New York local time\| America/New_York\|
-\| Los Angeles local time\| America/Los_Angeles\|
-\| London local time\| Europe/London\|
-\| UTC\| UTC\|

When creating a task in natural language, the default time zone is `Asia/Shanghai` if none is specified. For cross-time-zone scenarios, always specify the time zone explicitly. Do not rely on the client's or computer's time zone, and avoid abbreviations such as CST and PST where possible.

For requirements such as "every day at 9:00 AM in New York", use cron with `America/New_York` so the task is scheduled by local calendar time; do not simply convert it to a fixed UTC time. Locations such as New York, Los Angeles and London observe daylight saving time, and some local times may be skipped or repeated on transition days, so schedule routine tasks away from transition periods — for example, at 9:00 AM local time. The fixed interval `PT24H` means an interval of 24 hours, which is different from "every day at 9:00 AM local time", especially during daylight saving time transitions.

### 6.4 API configuration examples

For API integration, use the following `trigger_policy` configurations.

**Common scheduling rules at a glance**

| Requirement | type | expression | timezone |
| Every 5 minutes | interval | PT5M | Optional; specify it explicitly when using a local-time window |
| Every five-minute clock boundary | cron | */5 * * * * | Asia/Shanghai |
| Every day at 09:00 Beijing time | cron | 0 9 * * * | Asia/Shanghai |
| Monday through Friday at 09:00 New York local time | cron | 0 9 * * 1-5 | America/New_York |
| Every Monday at 10:00 Los Angeles local time | cron | 0 10 * * 1 | America/Los_Angeles |
| Monday through Friday, every five minutes from 09:00 through 17:55 | cron | */5 9-17 * * 1-5 | Asia/Shanghai |
| The 1st of every month at 09:00 Beijing time | cron | 0 9 1 * * | Asia/Shanghai |
| Run once at a specified time | once | 2027-05-01T15:00:00+08:00 | Optional because the timestamp already includes an offset |

Cron uses 5 fields, in this order: minute, hour, day of month, month, and day of week. It does not include a seconds field. The minimum interval for recurring tasks is 1 minute.

**Complete creation request: run every five minutes.** Replace the IDs below with your actual Identity, Template and Environment IDs; `QODER_PAT` is the caller's access token.

```
curl -sS -X POST 'https://api.qoder.com/api/v1/forward/schedules' \
  -H "Authorization: Bearer $QODER_PAT" \
  -H 'Content-Type: application/json' \
  -d '{
    "identity_id": "idn_xxx",
    "template_id": "tmpl_xxx",
    "environment_id": "env_xxx",
    "name": "Order Sync Check",
    "initial_events": [
      {
        "type": "user.message",
        "content": "Check failure records in the order synchronization system from the 5 minutes preceding the current check time. Summarize the number of failures, reasons, and order IDs; if there are no failures, briefly output the check results."
      }
    ],
    "trigger_policy": {
      "type": "interval",
      "expression": "PT5M"
    },
    "execution": {
      "session_mode": "new_session",
      "max_concurrent_runs": 1
    }
  }'
```

If no start time is configured, the first interval execution is scheduled one interval after successful creation, and subsequent executions advance according to the scheduled interval. This does not mean "wait five minutes after the previous run finishes".

**Alternative trigger policy: every day at 9:00 AM New York local time.** This is the value of the `trigger_policy` field inside the full creation request:

```
{
  "type": "cron",
  "expression": "0 9 * * *",
  "timezone": "America/New_York"
}
```

When calling the HTTP API directly, cron requires an explicit timezone; the natural language tool's default time zone rule does not replace this mandatory API requirement.

**Alternative trigger policy: every five minutes within a limited window.**

```
{
  "type": "interval",
  "expression": "PT5M",
  "timezone": "Asia/Shanghai",
  "start_at": "2027-05-01T09:00:00+08:00",
  "stop_at": "2027-05-01T18:00:00+08:00"
}
```

Create this task before the window begins. `start_at` and `stop_at` define the overall period during which the task is active. For recurring daily business hours, use cron's hour and day-of-week fields.

**Alternative trigger policy: run once at a specified time.**

```
{
  "type": "once",
  "expression": "2027-05-01T15:00:00+08:00"
}
```

The time must be later than the server's current time. Natural language supports expressions such as "in 30 minutes"; the HTTP creation API requires an absolute time for `once`, which the caller must calculate before submitting the request.

### 6.5 Manage tasks and view results

After successfully creating a task in natural language, check the task ID, scheduling rule, time zone and next scheduled execution time. You can then say:

```
List all my current scheduled tasks.
```

```
Change "Daily Industry Briefing" to run at 10:00 AM Beijing time, keeping all other settings unchanged.
```

```
Change "Order Sync Check" to run every 15 minutes, keeping the original task instructions.
```

```
Delete the "Release Window Health Check" task.
```

If multiple tasks have the same name, specify the task ID to identify the exact task. A natural language "delete" request archives the task, stops future triggers and retains historical execution records; it does not cancel executions already in progress.

**How to view results:**

- For tasks created in natural language in a regular web conversation, results are returned to the original conversation where the task was created.
- For tasks created in natural language in an IM Channel conversation, results are delivered to the corresponding Channel conversation.
- Tasks created through the API are not automatically linked to a chat conversation. Query **Schedule Runs** to retrieve results; configure sinks separately if IM delivery is required.

API clients can first call `POST /api/v1/forward/schedules/{schedule_id}/run` to trigger a manual test run, then use `GET /api/v1/forward/schedule_runs/{run_id}` to view the execution results. Successful task creation or a successful manual trigger does not mean execution has completed; check the run's status and error details. To temporarily stop and resume a Schedule, call its `/pause` and `/unpause` endpoints.

### 6.6 Tips for using Schedule effectively

- **Make task instructions self-contained.** Specify the data sources, items to process and output requirements. Avoid instructions such as "do what we just discussed". By default, each run uses a new execution Session and does not carry over the chat history; `reuse_session` reuses that Schedule's execution Session.
- **Configure files explicitly.** Chat attachments from the conversation where the task was created are not automatically copied to the Schedule. Use files configured in the Template or Identity config; Schedule-specific files must be configured through the API's `resources` field.
- **Match the check frequency to the execution duration.** By default, the maximum concurrency for a single Schedule is 1. If the previous run is still in progress, the next trigger may be recorded as skipped with the error `concurrency_limit_reached`. Keep high-frequency tasks short.
- **Account for data boundaries in periodic checks.** The "past five minutes" approach in the examples suits simple health checks. If data must not be missed or processed twice, design deduplication and recovery mechanisms using stable IDs from the data source, processing cursors or persistent state.
- **Specify an end time for temporary monitoring.** Running every five minutes around the clock produces 288 scheduled trigger points per day. Set the frequency and time window to match what you actually need.
- **Test before enabling long-term operation.** Verify data permissions, output content and where results are delivered. For external operations such as sending messages or writing data, implement deduplication and idempotency in your business application.

## 7. Create a dashboard

The judging rubric explicitly rewards dashboards and reports, and a dashboard is also the simplest way to show that your agent runs unattended.

🔧 **Build it locally first.**

1. In your project, ask Qoder to scaffold a web dashboard that reads from the Moomoo MCP/skills: positions, P&L, equity curve, open orders, drawdown and the agent's decision log. Adapt it to whatever works for you.
2. Check that it runs on your local machine; you can ask Qoder to start the dev server for you.

🔐 **Wire it to Cloud Agents.** The dashboard needs a Qoder **Personal Access Token** (PAT) to read Cloud Agents sessions and event logs.

To create a PAT:

1. Open [qoder.com/cloud/pat-keys](https://qoder.com/cloud/pat-keys) and click **Create token**.
2. Copy the token immediately — it is shown only once.
3. Send requests to `https://api.qoder.com/api/v1/cloud` with the token in the `Authorization: Bearer <PAT>` header, and only from your dashboard's server side.
4. Keep the token in a local `.env` file listed in `.gitignore`; never commit it or include it in client-side code.

🎥 **Bonus tip:** record a short screen capture of the local dashboard in action (you can ask Qoder to record it for you) and submit it with your entry.

## 8. Tips and tricks: fine-tuning agents

### 8.1 Keep a local copy and version history of your agents

Keep your own version history before updating an agent in Qoder Cloud Agents (QCA). Updates replace the active configuration, so the cloud template should never be your only record of a working version.

1. **Save and review locally.** Ask Qoder Desktop to retrieve the current agent configuration and document it in `AGENTS.md` within your project. Include the system prompt, model, tool permissions, MCP connections, skill bindings and sub-agent versions. Review the instructions and risk controls before making changes. Keep the exported prompts clearly separated from any instructions meant for the Desktop assistant, so the two are not confused.
2. **Add a timestamped comment.** Record the retrieval time, agent ID, cloud version and a brief change summary. Use the version returned by QCA rather than assigning one manually. If you have several agents, add a comment to each agent's section.
```
   <!--
   Retrieved at (UTC): <YYYY-MM-DDTHH:MM:SSZ>
   Agent ID: <agent ID>
   Cloud version: <version returned by QCA>
   Local revision: <your revision label>
   Change summary: <brief description>
   -->
```
3. **Own your version control.** Use local Git, a private GitHub repository or dated backup folders. Save the working configuration before every change, note why you changed it, and keep the exact version used for your final submission. Never include PATs, OAuth tokens or other credentials.
4. **Verify after each update.** Before publishing changes, compare the current cloud configuration with your local copy. After the update, retrieve it again, confirm that only the intended changes were applied, and refresh the timestamped record. When replacing configuration arrays, carry over the existing tool, MCP and skill bindings.

### 8.2 Tuning the agent

**Use subagents rather than one big agent.** A clean, scoreable structure is: a *researcher* (news, sentiment, unusual activity → candidate list), an *executor* (talks only to the paper account, and only after the guard passes), and a *risk auditor* whose sole job is to say no and write the daily drawdown report. Run the auditor in a separate session so it cannot be talked into agreeing. Add this to the orchestrator prompt: "never let the executor act on the researcher's output without the auditor's approval."

**Version everything you tune.** After each prompt or skill change, re-run the same three or four fixed evaluation prompts and diff the outputs before you let the change into your "production" agent. Pin the skill `version` on the agent that actually trades so a later upload cannot silently change its behaviour mid-competition; an unpinned `latest` binding is a real risk when judges replay your runs.

**Log decisions as a first-class artifact.** Have the agent append one structured line per decision — including the ones it *rejected* and why — to a file in the repo. Judges ask "what failed and why", and a rejection log answers it better than any slide. This also gives your dashboard something real to chart.

## 9. Let agents collaborate (Forward Mode)

In Forward Mode, one agent can act as a **coordinator**: it breaks a task into pieces and delegates them to **child agents**, each running in its own Session Thread with its own model, tools, and conversation history. The coordinator collects their results into the final response. You can also attach an **Advisor** — an independent model the coordinator consults for a second opinion at key steps.

![Diagram: a coordinator agent in a Forward Mode session delegates tasks to child agent threads, and consults an Advisor for a second opinion.](data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNjQwIDI3MiIgcm9sZT0iaW1nIiBhcmlhLWxhYmVsPSJEaWFncmFtOiBhIGNvb3JkaW5hdG9yIGFnZW50IGluIGEgRm9yd2FyZCBNb2RlIHNlc3Npb24gZGVsZWdhdGVzIHRhc2tzIHRvIGNoaWxkIGFnZW50IHRocmVhZHMsIGFuZCBjb25zdWx0cyBhbiBBZHZpc29yIGZvciBhIHNlY29uZCBvcGluaW9uLiI+PGRlZnM+PG1hcmtlciBpZD0iY29sbGFiLWFycm93IiB2aWV3Qm94PSIwIDAgMTAgMTAiIHJlZlg9IjkiIHJlZlk9IjUiIG1hcmtlcldpZHRoPSI3IiBtYXJrZXJIZWlnaHQ9IjciIG9yaWVudD0iYXV0by1zdGFydC1yZXZlcnNlIj48cGF0aCBkPSJNMCwwIEwxMCw1IEwwLDEwIHoiIGZpbGw9IiMyODZFNDciPjwvcGF0aD48L21hcmtlcj48L2RlZnM+PHJlY3QgeD0iOCIgeT0iOCIgd2lkdGg9IjYyNCIgaGVpZ2h0PSIyNTYiIHJ4PSIxMiIgZmlsbD0iI0Y2RkFGNyIgc3Ryb2tlPSIjMjg2RTQ3IiBzdHJva2Utd2lkdGg9IjEuNSIgc3Ryb2tlLWRhc2hhcnJheT0iNiA0Ij48L3JlY3Q+PHRleHQgeD0iMjQiIHk9IjM0IiBmb250LXNpemU9IjEyLjUiIGZpbGw9IiM1NzYyNUMiPkZvcndhcmQgTW9kZSBTZXNzaW9uIMK3IHNoYXJlZCBzYW5kYm94ICYjeDI2OyBmaWxlc3lzdGVtPC90ZXh0PiA8cmVjdCB4PSIxNzAiIHk9IjUyIiB3aWR0aD0iMTgwIiBoZWlnaHQ9IjQ2IiByeD0iOSIgZmlsbD0iIzI4NkU0NyI+PC9yZWN0Pjx0ZXh0IHg9IjI2MCIgeT0iODAiIGZvbnQtc2l6ZT0iMTQuNSIgZm9udC13ZWlnaHQ9IjcwMCIgZmlsbD0iI0ZGRkZGRiIgdGV4dC1hbmNob3I9Im1pZGRsZSI+Q29vcmRpbmF0b3I8L3RleHQ+IDxyZWN0IHg9IjQ3OCIgeT0iNTIiIHdpZHRoPSIxMzgiIGhlaWdodD0iNDYiIHJ4PSI5IiBmaWxsPSIjRkZGRkZGIiBzdHJva2U9IiMyODZFNDciIHN0cm9rZS13aWR0aD0iMS41IiBzdHJva2UtZGFzaGFycmF5PSI1IDQiPjwvcmVjdD48dGV4dCB4PSI1NDciIHk9Ijc0IiBmb250LXNpemU9IjE0IiBmb250LXdlaWdodD0iNzAwIiBmaWxsPSIjMjg2RTQ3IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIj5BZHZpc29yPC90ZXh0PiA8dGV4dCB4PSI1NDciIHk9IjkwIiBmb250LXNpemU9IjExIiBmaWxsPSIjNTc2MjVDIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIj5hZHZpY2Ugb25seTwvdGV4dD4gPGxpbmUgeDE9IjM1MCIgeTE9Ijc1IiB4Mj0iNDcyIiB5Mj0iNzUiIHN0cm9rZT0iIzI4NkU0NyIgc3Ryb2tlLXdpZHRoPSIxLjUiIHN0cm9rZS1kYXNoYXJyYXk9IjUgNCIgbWFya2VyLXN0YXJ0PSJ1cmwoI2NvbGxhYi1hcnJvdykiIG1hcmtlci1lbmQ9InVybCgjY29sbGFiLWFycm93KSI+PC9saW5lPjx0ZXh0IHg9IjQxMSIgeT0iNjYiIGZvbnQtc2l6ZT0iMTEiIGZpbGw9IiM1NzYyNUMiIHRleHQtYW5jaG9yPSJtaWRkbGUiPnNlY29uZCBvcGluaW9uPC90ZXh0PiA8bGluZSB4MT0iMjYwIiB5MT0iOTgiIHgyPSIxMTciIHkyPSIxNzIiIHN0cm9rZT0iIzI4NkU0NyIgc3Ryb2tlLXdpZHRoPSIxLjUiIG1hcmtlci1lbmQ9InVybCgjY29sbGFiLWFycm93KSI+PC9saW5lPjxsaW5lIHgxPSIyNjAiIHkxPSI5OCIgeDI9IjMyMCIgeTI9IjE3MiIgc3Ryb2tlPSIjMjg2RTQ3IiBzdHJva2Utd2lkdGg9IjEuNSIgbWFya2VyLWVuZD0idXJsKCNjb2xsYWItYXJyb3cpIj48L2xpbmU+PGxpbmUgeDE9IjI2MCIgeTE9Ijk4IiB4Mj0iNTIzIiB5Mj0iMTcyIiBzdHJva2U9IiMyODZFNDciIHN0cm9rZS13aWR0aD0iMS41IiBtYXJrZXItZW5kPSJ1cmwoI2NvbGxhYi1hcnJvdykiPjwvbGluZT48dGV4dCB4PSIzNTIiIHk9IjE0MiIgZm9udC1zaXplPSIxMS41IiBmaWxsPSIjNTc2MjVDIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIj5kZWxlZ2F0ZSDCtyBmb2xsb3cgdXA8L3RleHQ+IDxyZWN0IHg9IjMyIiB5PSIxNzYiIHdpZHRoPSIxNzAiIGhlaWdodD0iNTIiIHJ4PSI5IiBmaWxsPSIjRkZGRkZGIiBzdHJva2U9IiMyODZFNDciIHN0cm9rZS13aWR0aD0iMS41Ij48L3JlY3Q+PHRleHQgeD0iMTE3IiB5PSIxOTkiIGZvbnQtc2l6ZT0iMTMuNSIgZm9udC13ZWlnaHQ9IjcwMCIgZmlsbD0iIzA5MEEwQiIgdGV4dC1hbmNob3I9Im1pZGRsZSI+UmVzZWFyY2hlcjwvdGV4dD4gPHRleHQgeD0iMTE3IiB5PSIyMTYiIGZvbnQtc2l6ZT0iMTEiIGZpbGw9IiM1NzYyNUMiIHRleHQtYW5jaG9yPSJtaWRkbGUiPm93biBTZXNzaW9uIFRocmVhZDwvdGV4dD4gPHJlY3QgeD0iMjM1IiB5PSIxNzYiIHdpZHRoPSIxNzAiIGhlaWdodD0iNTIiIHJ4PSI5IiBmaWxsPSIjRkZGRkZGIiBzdHJva2U9IiMyODZFNDciIHN0cm9rZS13aWR0aD0iMS41Ij48L3JlY3Q+PHRleHQgeD0iMzIwIiB5PSIxOTkiIGZvbnQtc2l6ZT0iMTMuNSIgZm9udC13ZWlnaHQ9IjcwMCIgZmlsbD0iIzA5MEEwQiIgdGV4dC1hbmNob3I9Im1pZGRsZSI+RXhlY3V0b3I8L3RleHQ+IDx0ZXh0IHg9IjMyMCIgeT0iMjE2IiBmb250LXNpemU9IjExIiBmaWxsPSIjNTc2MjVDIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIj5vd24gU2Vzc2lvbiBUaHJlYWQ8L3RleHQ+IDxyZWN0IHg9IjQzOCIgeT0iMTc2IiB3aWR0aD0iMTcwIiBoZWlnaHQ9IjUyIiByeD0iOSIgZmlsbD0iI0ZGRkZGRiIgc3Ryb2tlPSIjMjg2RTQ3IiBzdHJva2Utd2lkdGg9IjEuNSI+PC9yZWN0Pjx0ZXh0IHg9IjUyMyIgeT0iMTk5IiBmb250LXNpemU9IjEzLjUiIGZvbnQtd2VpZ2h0PSI3MDAiIGZpbGw9IiMwOTBBMEIiIHRleHQtYW5jaG9yPSJtaWRkbGUiPlJpc2sgYXVkaXRvcjwvdGV4dD4gPHRleHQgeD0iNTIzIiB5PSIyMTYiIGZvbnQtc2l6ZT0iMTEiIGZpbGw9IiM1NzYyNUMiIHRleHQtYW5jaG9yPSJtaWRkbGUiPm93biBTZXNzaW9uIFRocmVhZDwvdGV4dD48L3N2Zz4=)

![Trading Agent template's Collaboration tab with a red arrow and circle highlighting the selected Portfolio Agent checkbox](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/images/19-agent-collaboration.png)

Template → Collaboration — Trading Agent with an Advisor and Portfolio Agent

**Best practices**

- Give each agent one clear role, and define who owns which files — all threads share one filesystem.
- State delegation criteria and output formats in the coordinator's system prompt. Selecting agents does not force delegation; the prompt does.
- Pin child agent versions instead of `latest`, so a mid-competition edit cannot silently change how a live session behaves.
- Grant credentials only to the agents that need them; the coordinator usually needs none.
- Use the Advisor for decisions that deserve a second opinion — it advises only and cannot take actions.

Full configuration reference: [https://docs.qoder.com/cloud-agents/multi-agents](https://docs.qoder.com/cloud-agents/multi-agents).

## 2026 Moomoo x Qoder AI Trading Agent Challenge

![Moomoo x Qoder AI Trading Agent Challenge event cover](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/images/16-event-cover.png)

### About

Calling all algo traders, AI builders, and developers: turn your trading ideas into working AI agents with Qoder and Moomoo. Build agents on the Qoder Cloud Agents platform to research the market, execute a strategy, and manage risk — then test and refine it in a paper-trading account powered by Moomoo.

Use Qoder to build your agents and skills and connect to the Moomoo MCP to test your approach with simulated funds. No live capital is required. The top 10 entries will be shortlisted for final judging.

### Prizes

Win over **S$8,500** worth of cash, trading vouchers and Qoder credits!

### Timeline

- 16 Nov 2026, 6:00–9:00 PM SGTKickoff Workshop with Qoder + Moomoo. Food, networking and AI trading insights; bring your laptop.

- 6:00 PM — Doors open. Visit the Moomoo booth (light refreshments served).
- 7:00 PM — Opening Address by Alibaba Cloud.
- 7:10 PM — Presentation by Moomoo.
- 7:20 PM — Introduction to Qoder and demo workshop with tips & hacks.
- 7:50 PM — Trading strategies sharing and introduction to the Moomoo API by a Moomoo in-house specialist.
- 8:45 PM — Q&A.
- 9:00 PM — End of event.

- 17–28 Nov 2026 Development and Trading window.

- 30 Nov 2026, 11:59 PM SGTSubmission deadline.

- 8 Dec 2026 Top 10 finalists presentation.

### What every approved participant receives

- A free one-month Qoder Pro Plan subscription (worth US$20) + 1,500 credits (worth US$20) to build and refine AI agents, linked to the email address used for your Luma registration.
- US$100,000 initial paper account balance.
- Access to the Moomoo MCP for the competition’s paper-trading account.

### Who can join

Open to all backgrounds — from algo traders and developers to AI builders and anyone curious about AI-powered trading.

New to Moomoo? Sign up at [https://j.moomoo.com/0t8aQP](https://j.moomoo.com/0t8aQP). For additional rewards, speak with the on-the-ground Moomoo staff or enter the Special Code **SG0189**.

### Judging criteria (subjected to change)

- **Risk-adjusted return (25%)** — Trading performance evaluated relative to the risks taken.
- **Qoder & Qoder Cloud Agent usage (30%)** — Effective use of Qoder and Qoder Cloud Agent for agent engineering, including multi-agent orchestration and automation, as well as developing dashboards, reports, and reusable skills.
- **Strategy & risk design (30%)** — A clear trading thesis and edge, defined conditions that invalidate the strategy, and robust risk controls, including position limits, drawdown responses, and kill switches.
- **Reusability & documentation (15%)** — Reference-ready agent templates, reusable skills and scripts, plus presentation slides or a report clearly explaining how the agent works.

### Submission

Submit by **30 November 2026, 11:59 PM SGT** through the submission link on the [Luma event page](https://luma.com/oezyv35j): a Qoder-generated presentation deck together with a runnable trading-agent package. Your submission should include your strategy explanation, risk limits, a log of trading decisions, trade fills and results, and a demo showing what worked, what failed, and why.

This competition uses simulated funds. Paper-trading performance does not predict live returns. Terms and conditions apply — see the [Moomoo Paper Trading Account Terms & Conditions](https://moomoo-qoder-challenge-rgkelnyuzbm.qoder.website/#) tab.

## Terms & Conditions

These Terms and Conditions ("Terms and Conditions") apply to the **2026 Moomoo x Qoder AI Trading Agent Challenge **("Activity") organised jointly by **Qoder** and **Moomoo Financial Singapore Pte. Ltd.** ("Moomoo SG"), a subsidiary of **Futu Holdings Limited** (collectively, the "Organiser").

1. **Eligibility**

- Participation is open to both new and existing users who hold a valid Moomoo SG Universal Account (“Moomoo SG Account”).
- Each participant must be a natural person aged 18 years and above and a resident of Singapore.
- Moomoo SG reserves the right to verify eligibility and disqualify participants at its sole discretion, without notice.

2. **Challenge Participation**

Subject to eligibility verification and compliance with these Terms, the five (5) participants with the highest final scores, as determined by the Judging Panel in accordance with the judging criteria set out in Clause 2, will be awarded the prizes set out in Clause 3.

Trading performance will be considered as part of the Challenge Rubric, but a participant will not be selected as a winner based solely on absolute investment returns, portfolio value or leaderboard position.

The Organisers reserve the right to verify participants' submissions, trading records, agent configurations and supporting documentation for the purposes of evaluating compliance with the Challenge requirements and validating the results.

### **Judging Criteria (subjected to change)**

- Risk-adjusted return (25%) — Trading performance evaluated relative to the risks taken.
- Qoder & Qoder Cloud Agent usage (30%) — Effective use of Qoder and Qoder Cloud Agent for agent engineering, including multi-agent orchestration and automation, as well as developing dashboards, reports, and reusable skills.
- Strategy & risk design (30%) — A clear trading thesis and edge, defined conditions that invalidate the strategy, and robust risk controls, including position limits, drawdown responses, and kill switches.
- Reusability & documentation (15%) — Reference-ready agent templates, reusable skills and scripts, plus presentation slides or a report clearly explaining how the agent works.

The Judging Panel's assessment and determination of the final scores and winners will be based on the stated judging criteria. The Organisers reserve the right to disqualify participants who breach these Terms and Conditions or engage in misconduct affecting the integrity of the Challenge.

3. **Prize Details**

-\| Final Ranking\| Total Prize Value\| Cash Award\| Moomoo Trading Coupon\|
-\| Rank 1\| S$3500\| S$2000\| 15 x S$100 Trading Coupon\|
-\| Rank 2\| S$2500\| S$1500\| 10 x S$100 Trading Coupon\|
-\| Rank 3\| S$1000\| S$500\| 5 x S$100 Trading Coupon\|
-\| Honorable mention\| S$500\| -\| 5 x S$100 Trading Coupon\|

- The “**Total Prize Value**” is the combined value of the Cash Award and the Trading Coupon. It is not a Cash Award plus an additional Trading Coupon of the same stated value.
- Each participant is eligible to receive only one prize under the Challenge.
- The prizes are personal, non-transferable, non-assignable and may not be exchanged, resold or converted into alternative benefits, except where the Organisers expressly agree otherwise in writing.
- The Cash Award will be funded and paid by the organising committee. The Trading Coupon will be issued by Moomoo SG, subject to these Terms and Moomoo SG’s applicable coupon rules.
- Each coupon has a minimum trade value of S$1 and a 365-day expiry upon issuance.
- The Organisers may substitute a prize, or any portion of it, with an alternative of equal or greater value where reasonably necessary, including where a prize cannot be issued due to legal, operational, compliance or product limitations.

#### **Terms and Conditions**

1. The Moomoo X Qoder AI Trading Agent paper trading account is purely a virtual trading account and can only be used for simulating trading challenges with US stocks, US stock ETFs and options；
2. The cash or other assets displayed in the Moomoo X Qoder AI Trading Agent Challenge account have no actual value and cannot be withdrawn or exchanged；
3. The content and design of the Moomoo X Qoder AI Trading Agent Challenge account are assets of the Organisers, participants are not allowed to alter, modify, adapt, imitate, or otherwise change any part in any way；
4. Participants acknowledge and agree that the Organisers may display or use their user nicknames, avatars, Moomoo App accounts, total returns, holdings, and trading information, as such information relates to the paper trading competition；
5. All transactions conducted through the Moomoo X Qoder AI Trading Agent Challenge account are virtual in nature. Instructions entered by participants will not be transmitted to any exchange for execution (including but not limited to the New York Stock Exchange, Nasdaq Stock Market, American Stock Exchange), nor will they constitute any settlement or payment obligations for participants or the company. Securities trading services provided by the company and any rights and obligations related to such services do not apply to virtual trading within the challenge account；
6. Some information displayed in the Moomoo X Qoder AI Trading Agent Challenge account (including security quotes) is provided by third parties. The organisers makes no representations, warranties, or commitments regarding the accuracy or completeness of such information and shall not be liable for any losses or damages incurred by any person directly or indirectly using such information；
7. The organisers has the final decision-making power to determine the winners of the Challenge based on judging criteria and weightings set out in these terms and conditions, the list of winners for each prize, and their prizes. Participants may not object to the organisers' decision;
8. If the organisers believes that a participant has engaged in any cheating behavior, the organisers has the right to cancel the results.
9. The organisers shall not be responsible for any errors, omissions, interruptions, deletions, defects, delays in transmission over communication lines, or any problems or technical malfunctions arising from telephone networks, computer online systems, servers or providers, computer equipment, software, or any technical issues or communication congestion resulting in failure to receive any emails or communications;
10. The organisers is not responsible for any damage or loss caused to participants or any other person's computer due to any form of human or non-human errors, including participation in the contest, instruction input and submission, or notification related to the contest, including damage or loss caused by computer viruses or harmful programs;
11. Some prizes for this activity are provided by third-party merchants (including items redeemed in the mall using points). Once the prize is collected, it cannot be returned or exchanged. The use of prizes is subject to the merchant's relevant terms. The winner shall bear all applicable taxes, fees, additional charges, and/or foreign tariffs (if any). In case of any issues with the prize, please contact the relevant merchant directly. The organisers assumes no legal responsibility;
12. Activity rewards are strictly distributed according to the rules. Participants cannot apply for rewards through special means if they do not meet the qualifications for the activity. The organisers reserves the final decision-making power on the distribution and changes of any rewards;
13. If the prizes for this activity are provided by Moomoo SG, their use is subject to the terms and conditions issued by Moomoo SG for the respective prizes;
14. There are expiration dates for receiving and using activity rewards. Failure to claim or use rewards within the specified period will result in the rewards being forfeited, and the winner is considered to have automatically waived their eligibility;
15. The organisers reserve the right to modify or cancel the activity process, rules, awards, explanations, etc., based on actual circumstances and will notify participants as early as possible. The interpretation of the rules of this activity belongs to the organisers, who has the right to modify rules, processes, etc., including but not limited to the rules and processes of the activity, in response to loopholes in the activity;
16. If the activity is not running normally for any reason, such as interruptions or early termination, the organisers has the right to make corresponding adjustments and handle trading operations during abnormal periods. Participants cannot object to the decisions made by the organisers;
17. The organisers may freely quote the achievements and personal information of participants in any promotions or advertisements related to the activity, including but not limited to name, portrait, or voice (except where prohibited by law), without the approval of the participant being quoted;
18. The confirmation of information and data for this activity is based on the organisers' backend confirmation, and the organisers reserves the final interpretation right;
19. This promotion does not constitute an offer, solicitation, advice, opinion, or any guarantee of securities, financial products, or tools.
20. The organisers reserve the final decision-making power on any disputes related to this activity;
21. All amounts for prizes denomination are in SGD dollars;
22. Each user is limited to using one account, one mobile phone number, and one device to participate in promotions. Abnormal behavior (including but not limited to using mobile phone device emulators and artificially modifying mobile phone device numbers) may automatically disqualify or suspend users’ eligibility for participating in the promotion.
23. This offer is limited to one reward per new account, with no more than one account enrolled per person；
24. You can only open one universal account with Moomoo SG. Moomoo SG does not allow to open a universal account on behalf of another person (i.e. non-beneficial owners are not allowed to open accounts). Please do not open the universal account if you are not the ultimate beneficial owner.
25. Each device, whether mobile or computer, can only receive one set of account opening bonus, deposit bonus and/or referral bonus. The same user can only be invited once. The same moomoo account, the same mobile phone number, and the same device are all regarded as representing the same user.
26. Any trademarks, graphic symbols, logos or intellectual property contained in any materials relating to this Challenge, particularly in connection with the rewards/prizes, are the property of their respective owners. Moomoo SG does not provide any financial advice, endorsement or sponsorship of its products or services.
27. Only one trading coupon can be used for a single order. In the event that multiple trading coupons are available in your account at the same time, trading coupons with the earliest expiration date shall be applied first. If two or more trading coupons share the same expiration date, the coupons with the higher face value shall be applied.
28. Trading coupons are unregistered, non-transferable, and each trading coupon can be used only once and applied to a single order.
29. Moomoo SG reserves the right to revoke or reclaim any trading coupon or cashback acquired by participants through means deemed inappropriate by Moomoo SG, including but not limited to exploiting system vulnerabilities, hacking, and false pretenses.
30. Trading coupon discount does not constitute an offer, solicitation, recommendation, opinion or any guarantee from Moomoo SG for any securities, financial products or tools. Investment is risky and you must be cautious when entering the market.
31. This Campaign/Promotion is not eligible to users whose names are on the "Moomoo SG Event Participation Ban List". If a user repeatedly violates safety rules of Moomoo SG, their name will be added to the "Moomoo SG Event Participation Ban List".
32. In the event of any inconsistency between these Terms and Conditions and any advertising, promotion, promotional and other materials related to or in connection with this Campaign/Promotion, these Terms and Conditions shall prevail.
33. Participants are responsible for the development, configuration and operation of any AI agents, scripts, automated tools or third-party applications used in connection with the Challenge. Participants must only use the tools, APIs, access permissions and functionalities authorised by the Organisers for the Challenge.
34. Participants are responsible for their AI agents, scripts and activities during the Challenge and must ensure compliance with these Terms and Conditions and applicable laws and regulations.
35. If you have any questions, please contact our online customer service team.
36. These Terms and Conditions have not been reviewed by the MAS.

## Moomoo Paper Trading Account Terms & Conditions

## 1. Eligible Products and Trading Hours

- Only **U.S.-listed stocks, ETFs, and options** may be traded. All other instruments are excluded.
- Trading is available during U.S. **pre-market, regular, and after-hours sessions**, from **4:00 AM to 8:00 PM ET**.

## 2. Account, Margin and Short Selling

- Each participant starts with **USD 100,000** in virtual funds.

- Margin trading and short selling are available.

- Margin requirements:

- **Long positions:** 50% initial margin; 40% maintenance margin.
- **Short positions:** 60% initial margin; 50% maintenance margin.

- Interest is charged daily after market close:

- Margin financing interest: **4.8% per annum**
- Short-selling interest: **6.0% per annum**

## 3. Trading and Position Limits

To support fair and orderly competition, the following restrictions apply:

- Stocks priced below **USD 1** are not eligible for trading.

- Stocks and options of companies with a market capitalisation below **USD 500 million** are not eligible for trading.

- A maximum of **200 executed orders per day** is permitted. Cancelled or amended orders are not included.

- Participants may hold a maximum of **100 positions** at any one time.

- Exposure to stock/ETF may not exceed 40% of total initial account assets. This limit will not apply where it is exceeded due to price movements or options exercise:

For example;

- Full Capital Utilization (100% Deployed): Because the limit applies to stock/ETF, you can deploy 100% of your $100k capital by splitting it across at least 3 different stocks/ETFs:
- Stock/ETF A: $40k (40%)
- Stock/ETF B: $40k (40%)
- Stock/ETF C: $20k (20%)
- (Or any split across 3+ tickers where no single ticker exceeds 40%, such as 35% / 35% / 30%, or 25% across 4 tickers).
- Exception for Options: currently not included in this 40% limit; the combined position + pending open orders for a single options contract are capped at 1,000 contracts
- Holding Cash is Optional: You do not have to leave 60% in cash. If you only hold 1 stock at 40%, the remaining 60% simply sits uninvested until you buy other tickers.

- Two Important Nuances in the Rules

- Active Buying vs. Passive Growth: The 40% limit only restricts you from buying more of a stock if that purchase pushes the position above 40% of your total account value. If you buy Stock A at 40% ($40k) and its price surges so that it becomes 45% of your account, you are not penalized and do not have to sell. You just won't be able to buy more of Stock A until its weight drops back below 40%.
- Holding vs. Just "Having Traded" 3 Tickers: Because the system blocks any single ticker from exceeding 40% of your assets, you cannot put 100% of your money into 1 or 2 stocks. To deploy your full capital at any given time, you must simultaneously hold at least 3 distinct tickers (assuming no single ticker has grown past 40% via price appreciation).

## 4. Risk Controls

- If remaining account liquidity falls below zero during trading hours, the system may initiate **forced liquidation**.
- Participants are responsible for monitoring their positions, liquidity and margin requirements at all times.

## 5. Option Expiry and Exercise

- All in-the-money (**ITM**) options expiring on a given day will be automatically exercised after market close.
- Where sufficient funds are available, the corresponding underlying securities will be bought or sold.
- If funds are insufficient, the system will execute all possible transactions and may forcibly liquidate positions as necessary to meet margin requirements.
- Out-of-the-money (**OTM**) options will expire worthless.
- Index and stock options will be settled using the market closing price on the expiry date.

## 6. Corporate Actions

- Supported corporate actions are limited to:

- Dividends
- Stock splits
- Reverse stock splits
- Ticker-symbol changes

- If a company is delisted, trading in that security will no longer be available. On the second business day after delisting, the system will credit virtual funds equal to the security’s last closing price to the participant’s competition account.

## 7. Order Matching

- The paper-trading system simulates actual market trade-by-trade volume.
- An order will not be filled merely because its price condition is met; matching market volume must also be available.
- Where actual market trade volume multiplied by 20 is less than the order quantity, the order may be partially filled. Any unfilled balance will remain pending until matched or cancelled.

## 8. Virtual Fees

All fees are simulated only and do not represent actual charges.

### Stocks

- Commission: **USD 0**
- Platform fee: **USD 0.99 per order**
- Transaction activity fee: **USD 0.000166 per share sold**, capped at **USD 8.30 per trade (applies to sell order only)**

### Options

- Commission:

- Option premium above USD 0.10: **USD 0.65 per contract**
- Option premium of USD 0.10 or below: **USD 0.15 per contract**
- Minimum commission: **USD 1.99 per order**

- Platform fee: **USD 0.30 per contract**

- Transaction activity fee: **USD 0.00279 per contract**

- Regulatory fee: **USD 0.015 per contract**

## 9. Competition Settlement

- Final results will be calculated using **regular-market closing prices on the final competition day**.
- The value of options exercised on the final day will be included in the final ranking.
- Trades executed during after-hours trading on the final day will not be included in competition results.
- Weekly return figures are based on prices as of **10:00 PM ET each Friday**.

## 10. Reset Card Prohibition and Disqualification

- The use of any **Reset Card**, revival feature, or equivalent mechanism to restore virtual funds is **strictly prohibited** during the competition.
- Any participant found to have used, attempted to use, or circumvented this restriction will be **automatically disqualified**.
- The organiser may revoke the participant’s results, eligibility, rewards and any related benefits.

## 11. Fair Play and System Integrity

- Participants who obtain profits through cheating, manipulation, unauthorised activity, or exploitation of system vulnerabilities will be disqualified, and their results and eligibility may be revoked.
- The paper-trading system is provided by moomoo. Where there is any discrepancy between simulated market data or results and the actual market, the **simulation system records and results will prevail**.

## FAQ

### Credits & benefits

#### What do I get for joining this competition?

Every approved participant receives a one-month Qoder Pro subscription, which includes 2,000 credits (worth US$20), plus a one-time add-on of 1,500 credits (worth US$20).

#### How do I claim my free one-time credit add-on pack?

You can claim it from [https://claims.sg-cloudace.com/](https://claims.sg-cloudace.com/).

#### What if I need more credits than what is provided?

You can purchase additional credits at 50% off, up to three times during the hackathon and no more than once per day. Only a limited number of discounted add-on packs are available, so they are offered on a first-come, first-served basis. Payment is accepted via PayNow QR or credit card through HitPay. You can claim your pack from [https://claims.sg-cloudace.com/](https://claims.sg-cloudace.com/).

### Participation, judging & prizes

#### Do I participate individually or as part of a team?

This is an individual competition.

#### What do the judges assess? Does “strategy and risk” refer to trading or AI agent design?

“Strategy and risk” focuses on trading strategy and financial risk management and accounts for 30% of the score. Judges also consider returns, trade execution, and your overall agent-based trading framework.

#### Can a high-return strategy lose marks if it takes excessive risk?

Strong returns do not guarantee a strong overall score. A high-risk approach may score lower on strategy and risk management, even if it is profitable.

#### What prizes are available?

Over **S$8,500** worth of cash, trading vouchers and Qoder credits are available.

### Setup & competition period

#### Can I stop trading and submit before the competition ends?

Yes. Early submission is allowed; you do not have to keep trading after deciding to submit. Your entry will still be assessed against the judging criteria.

#### What happens if my agent loses all the funds in the competition account during setup?

The competition account cannot be reset. You can still submit your work and earn points under the other judging criteria. To avoid using up competition funds while testing, practise with a separate paper trading account first.

### Paper trading account & market access

#### How and when will I receive access to the competition’s paper trading account?

The Moomoo team will enable the competition account for registered participants. Access will begin to roll out starting from **17 November 2026, 11:00 AM SGT**. You can confirm your access from the Papertrade section of your moomoo app. If you run into any issues, please contact the organizers through the WhatsApp group chat.

#### How do I connect Qoder to the correct paper trading account?

1. Connect Qoder to moomoo through the MCP and install the relevant skills.
2. During authentication, select **Market Data** as demonstrated in the briefing; do not select the live trading execution or account-order permissions.
3. Ask Qoder: “Which accounts can I access?” Paper trading accounts have their own identifiers, which the agent can read even if they are not visible in the app.
4. Identify and cross-check the competition account, especially if you have several paper trading accounts.
5. Explicitly tell Qoder to use only that account for subsequent competition trades, and verify the selected account before trading.

#### How can I test a trade before using the competition account?

Use a separate paper trading account and ask the agent to place a test trade. Check whether it fills, then test closing the position and reviewing the resulting profit or loss.

#### What market prices does the paper trading account use?

The paper trading account follows current market prices shown in moomoo, rather than a separate set of simulated prices. The briefing referred to the latest price and candlestick data. Available quote detail, such as bid–ask information, depends on your market-data access; refresh the display when needed.

#### Can I trade outside regular US market hours?

Yes, the US paper trading account supports pre-market and post-market trading as well as regular US market hours.

### Trading rules & risk controls

#### Who sets the agent’s risk limits?

You are responsible for defining your agent’s strategy-level risk controls. The briefing encouraged planning take-profit and stop-loss actions, and risk management forms part of the judging criteria.

#### What trading costs should I account for?

Use the commission rates in the participant handbook. Account for commissions and slippage when evaluating your strategy and recording trades in your journal.

#### Can I use multi-leg options strategies?

The briefing recommended single-leg trades and discussed placing multi-leg spreads as separate leg orders. Those orders use the order allowance, so factor that into your strategy.

### MCP, data & existing tools

#### How can I find out which tools the moomoo MCP provides?

Check the available-tools list in the MCP quick-start documentation. Once connected, you can also ask Qoder, “What can I do with this MCP?” to list the tools available to your agent.

#### Is historical options data available for backtesting through the moomoo MCP?

At the time of the briefing, historical options-data support was still being developed; the speakers said they were using current options data. For backtesting, you can connect other MCPs or supply external datasets and relevant skills.

#### Can I use my existing agents, databases, MCPs or reference materials?

Yes. You can integrate your existing setup by connecting MCPs to local Qoder or a Cloud Agent, and supplying reference materials through a knowledge base. Books, documents and presentation PDFs can also provide context. You must still use Qoder to build the competition entry.

#### How is moomoo AI different from an agent built with Qoder?

moomoo AI is a separate assistant that works with data in the moomoo app. You can use its research or stock shortlists as input to your Qoder agent. Building with Qoder lets you combine moomoo with third-party MCPs, skills and other tools in a customised agent workflow.

### Dashboard & agent hosting

#### Where can I host the dashboard and AI agents?

The dashboard can be deployed to Qoder Sites ([https://docs.qoder.com/qoder/sites](https://docs.qoder.com/qoder/sites)), while agents can run on Qoder Cloud Agents ([https://docs.qoder.com/cloud-agents/overview](https://docs.qoder.com/cloud-agents/overview)). Ask Qoder to deploy the dashboard to Qoder Sites in your chat. You may also keep the dashboard local; publishing it is not required for submission.

#### How do local Qoder and Cloud Agents work together?

Use local Qoder to design, build and refine your agents, then deploy them through the Cloud Agent console. Both use the same account. With the Qoder Cloud Agent connector, local Qoder can inspect and update the deployed agents. Scheduled cloud agents can keep running without your computer being switched on or a separate VPS.

#### How do I connect the moomoo MCP to a Cloud Agent?

Open the Cloud Agent’s **Connector** settings, add the moomoo MCP endpoint from the setup guide, and select **Connect** to complete authorisation. Install the required skills separately. The participant handbook contains the setup instructions; then verify that the agent can access the correct competition account.

#### How do I configure another Cloud Agent instance?

Agent instructions and configuration are defined in a template. Ask local Qoder to propose or adjust the template in natural language, then deploy it to Qoder Cloud Agents.

#### Do I need Qoder Wake for this competition?

No. QoderWake was described as a way to run a digital employee locally on your device. Cloud Agents provide a cloud runtime, so you do not need to supply hardware for the agent to keep running.

#### Must I use both local Qoder and Cloud Agents?

Yes, you must use both of them.

#### How do I let my Cloud Agents communicate with each other?

Enable **Collaboration** in the agent settings. If communication is not working, ask Qoder to inspect the configuration through its Cloud Agent connector.

#### How can agents share project context?

The briefing demonstrated shared workspace memory, including global and project memory, and a generated project wiki that other agents can read to understand and continue the work.

#### Can I set up and manage the project from my phone?

Yes, it is possible by linking Qoder mobile to desktop Qoder. However, setup and dashboard work are easier on a larger screen, so a phone-only workflow may be cumbersome.

### Scheduling & credit usage

#### Should every agent run on its own schedule?

Prefer a coordinator agent that runs on a schedule and triggers the other agents when needed, rather than scheduling every agent independently. A 15-minute interval was shown as an example, not a requirement.

#### Do local Qoder and Cloud Agents use the same account, and where can I check usage?

Yes, both use the same Qoder account. Check usage in your Qoder account or workbench and in the Cloud Agent’s **Observability** section. You can also ask Qoder about usage or add a usage view to your dashboard.

#### How can I reduce credit usage? Is Auto mode always the best choice?

Auto mode is not always necessary. Once the workflow is stable, assign lighter models to simpler tasks and reserve more capable models for work that needs them. Use a balanced configuration rather than running every agent in the most resource-intensive mode.

### Submission

#### What must I submit, and do I need a GitHub repository?

Hosting your files on GitHub is optional. At minimum, provide a readable link to a report or presentation generated with Qoder, such as an HTML report or PowerPoint presentation. Explain your agent design, trading strategy, risk controls and results clearly enough for the judges to assess them. The organisers can separately see the competition account’s returns and overall Qoder credit usage.

#### Do I have to publish or share access to my dashboard?

No. Your dashboard can remain private or run locally. Include screenshots in your final presentation or submit a generated HTML report instead.

### Materials & community

#### Will participants receive the presentation slides and session recording?

Yes. The [Qoder Deck](https://ngynckpj.qwenwork.page/), [Moomoo Deck](https://moomoo-strategy-briefing-j692pppjg7l.qoder.website/#s=1) and [Zoom Recording](https://drive.google.com/file/d/1e0s5JcAhRr6TaHqrzfXBHQb8FZBbnbMq/view) are available now. You can also find them at the top of the Participant Handbook.

#### Where can I find the prompt used to create the demo dashboard?

The dashboard prompt is included in the [Qoder Deck](https://ngynckpj.qwenwork.page/). You can use it as a starting point and refine the dashboard through further prompts.

## Disclaimer

This challenge is a simulation exercise. By registering and participating, you acknowledge and agree to the following.

1. **Paper trading only.** All trading must take place in a moomoo paper-trading (SIMULATE) account using simulated funds. Live brokerage accounts, real capital, and real order execution are outside the scope of this challenge and are not permitted. Do not point any agent you build here at a live account.
2. **Qoder is not a trading system, and is not responsible for its use.** Qoder, Qoder Cloud Agents, and the agents you build with them are experimental software provided for learning and demonstration. They are not investment advice, a recommendation, or a brokerage or execution service. Qoder accepts no responsibility or liability for any use of Qoder agents, in this challenge or afterwards — including any use connected to real accounts, real money, or automated order placement. You use these tools at your own risk and remain responsible for anything your agents do.
3. **Results are yours.** Any gain or loss — simulated in this challenge, real if you ever choose to trade live — depends entirely on your own strategy, prompts, configuration, risk limits, and trading decisions. Qoder does not control, direct, or endorse those decisions, and makes no claim about their outcome.
4. **Simulated performance is not predictive.** Rankings, returns, and dashboard figures reflect simulated fills under simulated conditions. They do not indicate what would happen with real capital, where fees, liquidity, latency, and slippage differ.
5. **Not financial advice.** Nothing in the challenge materials, talks, dashboards, or agent output constitutes financial, investment, legal, or tax advice. Consult a licensed professional before making real investment decisions.
6. **Compliance.** You are responsible for complying with moomoo's terms, market rules, and applicable law, and for any third-party data or API terms you use. Entries that breach the rules above may be disqualified.

Participation is at your own risk. The organizers' decisions on eligibility, ranking, and disqualification are final.
