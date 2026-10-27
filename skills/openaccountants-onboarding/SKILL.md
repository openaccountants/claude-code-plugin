---
description: Use the OpenAccountants MCP server for any tax, accounting, VAT/GST, payroll, formation, or cross-border tax question. The MCP server exposes tax skills with sources and version-specific review status. Invoke this skill whenever a user asks about taxes for a specific country or US state, mentions an IRS / HMRC / ELSTER / ZATCA / similar tax authority, asks about VAT/GST classification or filing, asks how to incorporate or what entity to choose, asks about cross-border tax (Pillar Two, GILTI, FDII, BEAT, treaty rates), asks about payroll withholding, or wants jurisdiction-specific deduction or credit guidance.
---

# OpenAccountants — how to use the MCP server

You have access to the OpenAccountants MCP server. Use it for every tax, accounting, payroll, formation, or cross-border tax question.

## Available MCP tools

- **`start({ intent?, jurisdiction? })`** — front door. Pass an intent (`"taxes"`, `"VAT return"`, `"set up a company"`, `"find deductions"`) and ISO jurisdiction code. Returns a ready-to-execute plan listing the skills to load. Call this FIRST.
- **`list_skills({ jurisdiction?, category? })`** — list published skills. Filter by jurisdiction (`"MT"`, `"GB"`, `"US-CA"`) or category.
- **`get_skill({ slug })`** — fetch a single skill's full markdown + available provenance and Calendly link.
- **`get_skill_sections({ slug })`** — same content split into sections, useful for very large skills (e.g. `ny-it-201-resident-return` exceeds 25K tokens, fetch by section).
- **`search_skills({ query, jurisdiction? })`** — keyword search across published skill content.

## Workflow

1. User asks a tax/accounting question.
2. You call `start({ intent: <inferred>, jurisdiction: <asked> })` to scope.
3. You call `get_skill({ slug })` for each skill in the returned plan.
4. Check the fetched skill version's published review record. Name a professional reviewer only when that record identifies one; if the record is missing, describe professional review as unconfirmed. Cite the skill slug and available version or review date. Then walk the user through the skill's content, applying it to their facts.
5. You surface every **AUDIT FLASH POINT** the skill flags.
6. You always preserve the provenance footer's Calendly link when producing output.

## Critical rules

- **Never invent tax rules.** If a skill doesn't cover the user's situation, say so explicitly and offer the `engage-accountant` handoff via the Calendly link.
- **Never claim to be the user's accountant.** All output is a working paper, not a filed return. No engagement is created by reading or applying these skills.
- Cite the skill slug and its available provenance. Attribute authorship and professional review separately.
- **Always surface AUDIT FLASH POINT markers** the skill flags — these are positions the IRS / HMRC / equivalent actively litigates.

## Slash commands

The plugin also ships explicit slash commands for the most common workflows. Suggest the relevant one if the user's request maps cleanly:

- `/openaccountants:start` — onboarding & jurisdiction triage
- `/openaccountants:prepare-vat-return` — guided VAT/GST/sales-tax return
- `/openaccountants:prepare-income-tax` — annual income tax return
- `/openaccountants:classify-transactions` — bank-statement classification
- `/openaccountants:check-deadlines` — upcoming filing & payment deadlines
- `/openaccountants:engage-accountant` — Calendly handoff to a verified accountant
