---
description: Connect the user with a verified accountant in their jurisdiction for review or formal engagement.
---

# Engage a verified accountant

The user said: $ARGUMENTS

OpenAccountants provides source-available tax skills and AI tooling. For anything that requires liability, sign-off, or formal advice, the user needs a human accountant.

1. From `$ARGUMENTS`, identify the jurisdiction(s) and a one-line summary of what the user needs (return review, tax planning, formation, payroll setup, etc.). Ask if missing.

2. List the verified accountants for that jurisdiction:
   - Open `https://www.openaccountants.com/network` and surface the listings
   - Or call `list_skills({ jurisdiction: "<code>" })` and identify professional reviewers only from each fetched skill version's published review record; this is not a complete accountant directory

3. Hand off to the booking flow:
   - The central Calendly link is `https://calendly.com/openaccountants-info/30min`
   - The booking team routes the user to the right named verifier
   - First call is free, 30 minutes, no obligation, no liability until both sides sign an engagement letter

4. Tell the user clearly:
   - This skill / chat does not create a client–accountant relationship
   - No liability attaches to anyone until you and the chosen accountant sign a formal engagement
   - The verified accountants list at `/network` is the source of truth for who's licensed in which jurisdiction
