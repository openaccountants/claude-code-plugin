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

### From the community marketplace (once approved)

```
/plugin install openaccountants@claude-community
```

### From this repo directly (works today)

```bash
/plugin marketplace add openaccountants/claude-code-plugin
/plugin install openaccountants@openaccountants
```

### Local dev / test

```bash
claude --plugin-dir ./openaccountants-claude-code-plugin
```

## Try it

After install, ask Claude:

> *I'm a YC founder with a Delaware C-corp planning to sell. Walk me through Section 1202 QSBS with the OBBBA 2025 changes.*

Claude will automatically:
1. Call `start({intent: "QSBS", jurisdiction: "US"})` (via the auto-invoked Skill)
2. Call `get_skill({slug: "us-section-1202-qsbs"})`
3. Walk you through the OBBBA-2025 tiered exclusion, the $75M asset cap, the SSTB exclusion list, California non-conformity, and the family-stacking strategy
4. Surface AUDIT FLASH POINT markers
5. End with the verified accountant's Calendly link

## What's under the hood

All commands and the onboarding skill ultimately call the **public OpenAccountants MCP server** at `https://www.openaccountants.com/api/mcp`. The server exposes 5 tools:

| Tool | Purpose |
|---|---|
| `start` | Pass intent + jurisdiction → ready-to-execute plan |
| `list_skills` | List published skills by jurisdiction / category |
| `get_skill` | Fetch one skill with full markdown + provenance footer |
| `get_skill_sections` | Same content split into sections (for skills > 25K tokens) |
| `search_skills` | Keyword search across published content |

All read-only. No auth, no signup, rate-limited at 60 req/min/IP.

## Jurisdictions

Deep packs for: **Malta · UK · Germany · Italy · France · Spain · Portugal · Ireland · Netherlands · US federal + 24 deep state packs (CA, NY, TX, FL, IL, OH, PA, MA, NJ, NC, MI, OR, WA, NH, DE, VA, GA, AZ, CO, NV, MN, MO, MD…) · Canada federal + provincial · India · Indonesia · China (in 简体中文) · Pakistan · Brazil (in PT-BR) · Saudi Arabia · South Africa · Nigeria · Kenya**

Plus cross-border matrices (PTE elections, sales-tax nexus, bonus depreciation conformity, 1099-K thresholds, FATCA/FBAR, GILTI/FDII/BEAT, P.L. 86-272 income-tax nexus).

Every other UN member state has at least foundational coverage.

## Important

These skills produce **working papers, not filed returns**. Every output preserves a "Talk to a verified accountant" footer with a Calendly link. No client–accountant relationship is created by reading or applying these skills — that requires a formal engagement letter signed by both you and a verified accountant.

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
