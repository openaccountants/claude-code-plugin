---
description: Prepare a VAT, GST, or sales-tax return for a specific jurisdiction using OpenAccountants skills with version-specific review status.
---

# Prepare a VAT / GST / sales-tax return

The user said: $ARGUMENTS

1. Identify the jurisdiction (Malta, UK, Germany, Italy, India GST, US-CA sales tax, etc.) and the period (e.g. `Q1 2025`, `January 2025`) from `$ARGUMENTS`. If missing, ask the user.

2. Use the OpenAccountants MCP tools to load the right skill:
   - `search_skills({ query: "VAT return", jurisdiction: "<ISO code>" })` to find the right slug
   - `get_skill({ slug: "<chosen slug>" })` to load the full skill content
   - For EU jurisdictions, also load `eu-vat-directive` and `vat-workflow-base`

3. Apply the loaded skill's classification rules to the user's transactions or invoices.

4. Produce a working paper showing:
   - Each transaction classified by VAT box / code
   - Box totals
   - Reconciliation against gross receipts
   - Deadlines and filing mechanics for the jurisdiction
   - Available skill provenance and Calendly link; name a reviewer only when the fetched version's published review record identifies one

5. Surface every **AUDIT FLASH POINT** marker the skill flags.

6. Remind the user this is a working paper, not a filed return — they must have a qualified professional review before filing. The skill's "Talk to a verified accountant" footer carries the Calendly link.

**Out of scope** unless the skill explicitly covers them: cross-border OSS/IOSS, margin schemes, partial exemption, VAT groups, capital goods scheme.
