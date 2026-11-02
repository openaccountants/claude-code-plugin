# OpenAccountants — Claude Code plugin

Connect Claude Code to OpenAccountants tax skills via MCP, with slash commands for tax and accounting workflows.

Skills include accountant-reviewed versions and source-cited drafts. Check the [current catalogue](https://www.openaccountants.com/skills) and [review method](https://www.openaccountants.com/review-method) for each skill's review status, reviewer, version and review date. Authorship or a jurisdiction lead's name does not establish professional review of every skill version.

## What you get

| Slash command | What it does |
|---|---|
| `/openaccountants:start` | Onboarding — figures out which jurisdiction + workflow applies |
| `/openaccountants:prepare-vat-return` | Guided VAT / GST / sales-tax return preparation |
| `/openaccountants:prepare-income-tax` | Annual income tax return for any jurisdiction |
| `/openaccountants:classify-transactions` | Bank-statement → categorized P&L using local chart of accounts |
| `/openaccountants:check-deadlines` | Upcoming filing & payment deadlines |
| `/openaccountants:engage-accountant` | Hand off to a verified human accountant |

Plus an **auto-invoked Agent Skill** at `skills/openaccountants-onboarding/SKILL.md` — Claude will reach for the MCP tools any time the user asks a tax/accounting question, even without an explicit slash command.

## Install

Clone the plugin and load the checkout for the current Claude Code session:

```bash
git clone https://github.com/openaccountants/claude-code-plugin.git openaccountants-claude-code-plugin
claude --plugin-dir ./openaccountants-claude-code-plugin
```

The directory must be the plugin root containing `.claude-plugin/plugin.json`. This repository does not contain a marketplace catalogue, so it cannot itself be added with `/plugin marketplace add`.

## Try it

After loading the plugin, ask Claude:

> Help me prepare an Australian GST/BAS working paper for the quarter ending 30 September 2026.

Claude will use `start` with the question, confirmed period and jurisdiction `AU`, fetch the exact returned skill slugs and retrieve relevant deferred sections. Before applying a skill, it checks the jurisdiction, period, sources and version-specific review record. It cites available provenance, states evidence gaps and offers an accountant contact link when requested.

## What's under the hood

All commands and the onboarding skill ultimately call the **public OpenAccountants MCP server** at `https://www.openaccountants.com/api/mcp`. The following 5 retrieval tools are part of a larger tool inventory. Discover the current advertised schemas before use:

| Tool | Purpose |
|---|---|
| `start` | Required intent and optional jurisdiction scope a question |
| `list_skills` | Browse by jurisdiction, domain or role; follow `next_offset` with the same filters |
| `get_skill` | Fetch a skill version, available provenance and section index |
| `get_skill_sections` | Fetch deferred sections needed for the question |
| `search_skills` | Keyword search across published content |

For a capability question with no tax intent yet, use the advertised `start_help` tool. Other tools can save or send information, so do not assume the complete server is read-only. Discovery requests should contain only non-identifying scope, not bank statements, taxpayer identifiers or full working papers. Saving or sending content requires the user’s explicit agreement to the destination and specific information. See the [privacy policy](https://www.openaccountants.com/privacy).

## Jurisdictions

Deep packs for: **Malta · UK · Germany · Italy · France · Spain · Portugal · Ireland · Netherlands · US federal + 24 deep state packs (CA, NY, TX, FL, IL, OH, PA, MA, NJ, NC, MI, OR, WA, NH, DE, VA, GA, AZ, CO, NV, MN, MO, MD…) · Canada federal + provincial · India · Indonesia · China (in 简体中文) · Pakistan · Brazil (in PT-BR) · Saudi Arabia · South Africa · Nigeria · Kenya**

Plus cross-border matrices (PTE elections, sales-tax nexus, bonus depreciation conformity, 1099-K thresholds, FATCA/FBAR, GILTI/FDII/BEAT, P.L. 86-272 income-tax nexus).

Every other UN member state has at least foundational coverage.

## Important

These skills produce **working papers, not filed returns**. Check each fetched version’s applicability, sources and published review record before using it. Preserve available provenance and contact links; do not invent a reviewer or booking link. Reading or applying skills does not create an engagement. Have a qualified professional review before filing or relying on a working paper.

## Licence

MIT for this plugin wrapper. Skill content has separate terms from this wrapper. The source repository's [licensing document](https://github.com/openaccountants/openaccountants/blob/main/LICENSING.md) describes the source-available Open Accountants Skills License, commercial options, third-party copyleft exceptions and prior AGPL releases. Check the terms for the skill version you use.

## Links

- Website: [openaccountants.com](https://www.openaccountants.com)
- Skills source: [github.com/openaccountants/openaccountants](https://github.com/openaccountants/openaccountants)
- MCP server: `https://www.openaccountants.com/api/mcp`
- Universal MCP server-card: `https://www.openaccountants.com/.well-known/mcp/server-card.json`
- Verified accountant network: [openaccountants.com/network](https://www.openaccountants.com/network)
- Book a verified accountant: [calendly.com/openaccountants-info/30min](https://calendly.com/openaccountants-info/30min)
- Cursor plugin (same MCP, different IDE): [github.com/openaccountants/cursor-plugin](https://github.com/openaccountants/cursor-plugin)
- LangChain example: [github.com/openaccountants/langchain-example](https://github.com/openaccountants/langchain-example)
