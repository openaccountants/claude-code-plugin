---
description: List upcoming tax filing and payment deadlines for a specific jurisdiction and taxpayer profile.
---

# Check upcoming tax deadlines

The user said: $ARGUMENTS

1. Identify the jurisdiction, taxpayer profile and exact date window from the user’s request or ask for them. Resolve relative terms such as ‘this quarter’ to dates.

2. Load the deadline-bearing skills via MCP:
   - Call `start({ intent: "Check filing and payment deadlines for <taxpayer profile> during <confirmed date window>", jurisdiction: "<code>" })`.
   - Call `get_skill({ slug })` for each exact slug in `skills_to_load`. If further discovery is needed, use `search_skills({ query: "deadline", jurisdiction: "<code>" })` and fetch the selected exact slugs too; search snippets alone are not enough to construct the calendar.
   - Check the fetched version’s jurisdiction, applicable period and sources before applying it. Retrieve any deferred sections needed for this question with `get_skill_sections` using the advertised schema. Resolve an outdated or inapplicable version first; state unresolved gaps rather than substituting training data.

3. Produce a chronological calendar showing the supported date, obligation, form and source skill slug. Include penalties only when supported by the fetched sources; mark unsupported fields as unconfirmed. Distinguish filing and payment dates and any conditions or extensions.

4. Highlight deadlines within the next 30 days as `URGENT`, using the user’s confirmed date window and the current date. Surface relevant warnings and jurisdiction-specific conditions from the skills. Cite each skill slug and its available version or review date. Attribute authorship and professional review separately, naming a reviewer only when the version’s published review record identifies one. Preserve available provenance and contact links; do not invent a reviewer or booking link.

5. Offer an available accountant contact link if the user wants professional help. This calendar is a working paper and requires professional review before reliance.

Use only non-identifying scope in MCP discovery requests. These steps do not authorise saving or sending the user’s records or contacting OpenAccountants.
