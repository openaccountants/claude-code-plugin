---
description: Prepare a VAT, GST, or sales-tax return for a specific jurisdiction using OpenAccountants skills with version-specific review status.
---

# Prepare a VAT / GST / sales-tax return

The user said: $ARGUMENTS

1. Identify the jurisdiction and the exact reporting period from the user’s request or ask for them. Use the local tax name, such as GST for Australia.

2. Use the OpenAccountants MCP tools:
   - Call `start({ intent: "Prepare the <VAT/GST/sales-tax> return for <confirmed period>", jurisdiction: "<code>" })`, including any specific question.
   - Call `get_skill({ slug })` for each exact slug returned in `skills_to_load`. Do not construct a jurisdiction-based slug.
   - For EU jurisdictions, also load `eu-vat-directive` and `vat-workflow-base`, checking their applicability before use.
   - Check the fetched version’s jurisdiction, applicable period and sources before applying it. Retrieve any deferred sections needed for this question with `get_skill_sections` using the advertised schema. Resolve an outdated or inapplicable version first; state unresolved gaps rather than substituting training data.

3. Apply the supported classification and calculation rules to the transactions or invoices. Load any dependencies identified by the fetched skills before using them.

4. Produce a working paper with transaction classifications, applicable return boxes, totals, reconciliation, deadlines and filing mechanics. Include only fields supported by the fetched sources for that period and identify missing evidence. Surface relevant **AUDIT FLASH POINT** markers. Cite each skill slug and its available version or review date. Attribute authorship and professional review separately, naming a reviewer only when the version’s published review record identifies one. Preserve available provenance and contact links; do not invent a reviewer or booking link.

5. Remind the user that the working paper is not a filed return and a qualified professional must review before filing. Offer an available accountant contact link if requested.

Cross-border OSS/IOSS, margin schemes, partial exemption, VAT groups and capital goods schemes require skills that explicitly cover them. Do not apply a generic return skill beyond its stated scope.

Use only non-identifying scope in MCP discovery requests. These steps do not authorise saving or sending the user’s records or contacting OpenAccountants.
