---
description: Onboarding for OpenAccountants — figure out which jurisdiction and tax workflow applies. Invoke this first when a user asks for tax/accounting help.
---

# Start an OpenAccountants tax workflow

The user said: $ARGUMENTS

Use the OpenAccountants MCP server to scope the user’s question.

1. If there is no tax or accounting question yet, use `start_help({})` for capability information or ask locally what the user wants. Do not call `start` without its required intent.
2. When the question is known, call `start({ intent, jurisdiction })`. Include the confirmed financial or assessment year or reporting period in the intent when relevant. Pass the jurisdiction when known (for example `AU`, `GB` or `US-CA`); otherwise omit it and follow the returned clarification.
3. Once the response is ready, call `get_skill({ slug })` for every exact slug in `skills_to_load`. Check the fetched version’s jurisdiction, applicable period and sources before applying it. Retrieve any deferred sections needed for this question with `get_skill_sections` using the advertised schema. Resolve an outdated or inapplicable version first; state unresolved gaps rather than substituting training data.
4. Walk through the supported content and surface relevant **AUDIT FLASH POINT** markers. Cite each skill slug and its available version or review date. Attribute authorship and professional review separately, naming a reviewer only when the version’s published review record identifies one. Preserve available provenance and contact links; do not invent a reviewer or booking link.

Outputs are working papers, not filed returns. Have a qualified professional review before filing or relying on them. Use only non-identifying scope in MCP discovery requests. These steps do not authorise saving or sending the user’s records or contacting OpenAccountants.
