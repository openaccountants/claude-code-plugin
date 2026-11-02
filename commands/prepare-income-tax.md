---
description: Prepare an annual income tax return for an individual or entity using OpenAccountants skills with version-specific review status for the relevant jurisdiction.
---

# Prepare an annual income tax return

The user said: $ARGUMENTS

1. Identify from the user’s request or ask for the jurisdiction, entity type and tax year. Do not guess a missing year.

2. Use the OpenAccountants MCP tools:
   - `start({ intent: "Prepare the <entity type> income tax return for <confirmed tax year>", jurisdiction: "<code>" })` to obtain the plan. Preserve the user’s specific question in the intent where relevant.
   - For each exact slug in `skills_to_load`, call `get_skill({ slug })`.
   - Check the fetched version’s jurisdiction, applicable period and sources before applying it. Retrieve any deferred sections needed for this question with `get_skill_sections` using the advertised schema. Resolve an outdated or inapplicable version first; state unresolved gaps rather than substituting training data.

3. Apply the supported skills to the user’s income, deductions and credits. Follow the loaded worksheet structure where available.

4. Produce a working paper showing:
   - Income computation
   - Deductions and credits with skill section citations
   - Tax computation with applicable brackets and rates
   - Estimated tax or safe harbour analysis where supported
   - Filing deadlines and forms supported for that period
   - Relevant **AUDIT FLASH POINT** markers
   - Cite each skill slug and its available version or review date. Attribute authorship and professional review separately, naming a reviewer only when the version’s published review record identifies one. Preserve available provenance and contact links; do not invent a reviewer or booking link.

5. Remind the user that the working paper is not a filed return and a qualified professional must review before filing. Offer an available accountant contact link if requested.

Use only non-identifying scope in MCP discovery requests. These steps do not authorise saving or sending the user’s records or contacting OpenAccountants.
