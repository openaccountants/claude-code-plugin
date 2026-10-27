---
description: Onboarding for OpenAccountants — figure out which jurisdiction and tax workflow applies. Invoke this first when a user asks for tax/accounting help.
---

# Start an OpenAccountants tax workflow

The user said: $ARGUMENTS

Use the `start` tool from the OpenAccountants MCP server to scope the workflow:

1. If the user already mentioned a jurisdiction (country / US state) and a clear intent (taxes, VAT return, formation, deductions), call `start({ intent, jurisdiction })` with ISO codes (e.g. `MT`, `GB`, `US-CA`).
2. If either is missing, call `start()` with no args to see what fields are needed, then ask the user to clarify.
3. Once `start` returns `status: "ready"`, walk through the `skills_to_load` array — for each slug, call `get_skill({ slug })` to fetch the full content, then apply it to the user's facts.
4. Check the fetched skill version's published review record. Name a professional reviewer only when that record identifies one; if the record is missing, describe professional review as unconfirmed. Cite the skill slug and available version or review date. Preserve the available provenance and Calendly link in your final response.

If the user is non-technical, prefer the more specific commands:
- `/openaccountants:prepare-vat-return`
- `/openaccountants:prepare-income-tax`
- `/openaccountants:classify-transactions`
- `/openaccountants:check-deadlines`
- `/openaccountants:engage-accountant`
