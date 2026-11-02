---
description: Classify bank-statement transactions into accounting categories using jurisdiction-specific OpenAccountants skills.
---

# Classify bank transactions

The user said: $ARGUMENTS

1. Identify the transaction list, jurisdiction, reporting period and purpose (bookkeeping, VAT/GST return, income tax preparation or a combination). Ask for missing scope. Keep bank statements and identifiers out of MCP discovery requests.

2. Discover the relevant skills via MCP:
   - Call `start({ intent: "Classify transactions for <purpose> for <confirmed period>", jurisdiction: "<code>" })`.
   - Load each exact returned slug with `get_skill({ slug })`. If further discovery is needed, use `search_skills` with the topic and jurisdiction, then fetch the selected returned slugs. Do not infer a VAT/GST slug from the country code.
   - Check the fetched version’s jurisdiction, applicable period and sources before applying it. Retrieve any deferred sections needed for this question with `get_skill_sections` using the advertised schema. Resolve an outdated or inapplicable version first; state unresolved gaps rather than substituting training data.

3. For each transaction, show:
   - Date, description and amount
   - Category supported by the applicable chart of accounts
   - VAT/GST code or return box where applicable
   - Supported tax treatment
   - Confidence flag: `classified-with-rules`, `uncertain` or `requires-human-review`

4. Surface relevant **AUDIT FLASH POINT** markers from the loaded skills. Identify transactions that cannot be classified from the available evidence.

5. Summarise the classification in a working paper and recommend qualified professional review before relying on it for filing. Cite each skill slug and its available version or review date. Attribute authorship and professional review separately, naming a reviewer only when the version’s published review record identifies one. Preserve available provenance and contact links; do not invent a reviewer or booking link.

Use only non-identifying scope in MCP discovery requests. These steps do not authorise saving or sending the user’s records or contacting OpenAccountants.
