# Sofia Master Prompt — Changelog (v4.0 – v4.2)

This changelog documents the bug-fix and platform changes made across versions 4.0, 4.1, and 4.2 of Sofia's Master Prompt. It is intended as a supporting record alongside the version-tagged prompt files in this repository.

---

## v4.0 — July 5, 2026
**Type:** Bug fix release

### Problem
Sofia had begun producing the wrong spiritual content type — for example, a "Personal Devotion" request would return content structured as D'Group / Discipleship Material instead. Re-prompting sometimes made Sofia explicitly state she was "running again using D'Group template," even when D'Group was never requested.

### Root causes identified
1. **Ambiguous activation logic.** Personal Devotion and D'Group content shared the same Role 1 activation word list ("devotion," "Dgroup"), with no rule telling Sofia which specific content structure to produce once Role 1 was active.
2. **Anchored example text.** The prompt's Transparency Rule contained exactly one worked example, and that example hardcoded the phrase "Using your Dgroup template structure..." With no other example to draw from, Sofia tended to reuse this exact phrase regardless of what was actually requested.
3. **Competing role specification.** A separate project documentation file (an authorship/IP record intended for GitHub and LinkedIn) defined its own, different set of Sofia's roles — different names, different count, different structure — from the Master Prompt. When present in Sofia's active knowledge base at the same time as the Master Prompt, this created two contradictory "sources of truth" for Sofia's role architecture.

### Fixes applied
1. Each spiritual content type (Personal Devotion / D'Group Material / Event Material) now has its own exact, non-overlapping trigger phrase and an explicit selection table. If a request doesn't clearly match one of the three phrases, Sofia now asks a direct clarifying question instead of guessing or defaulting to the last-used type.
2. The Transparency Rule's example was de-anchored: it now shows multiple worked examples across all three content types and instructs Sofia to always match the bracketed content type to exactly what was requested in the current message — never to a prior request or a prompt example.
3. Added a **Single Source of Truth Rule**: only the Master Prompt governs Sofia's roles, activation logic, and behavior. Separate authorship/portfolio/IP documents are explicitly marked as external records only, never to be treated as a second role specification, even if accidentally present in Sofia's knowledge base.

---

## v4.1 — July 5, 2026
**Type:** Versioning update only

No content changes from v4.0. Filename and internal version header updated for repository documentation consistency (matching the intended GitHub versioning scheme).

---

## v4.2 — July 5, 2026
**Type:** Platform-agnostic release

### Problem
The Master Prompt hardcoded a requirement that Sofia "ONLY performs correctly on claude.ai (Claude by Anthropic)" and instructed Sofia to identify herself as "built on Claude by Anthropic." In practice, Sofia has been running on **Gemini (Gemini Gems)** since inception — a free, widely accessible platform — creating a direct contradiction between the prompt's stated platform and its actual runtime environment. This mismatch was a plausible contributing factor to instability, since the prompt was describing a platform and identity that didn't match where Sofia was actually deployed.

### Fix applied
- Removed the claude.ai-only platform requirement entirely.
- Replaced it with an explicit platform-agnostic statement: Sofia is designed to run on any capable AI model or agent platform (Gemini, Claude, ChatGPT, or others), and the underlying model is simply the engine powering her — it does not change her identity, roles, or behavior.
- Rewrote Sofia's self-identification statement to remove the "built on Claude by Anthropic" claim, replacing it with platform-neutral language.
- Generalized a learning-resource reference that previously pointed only to Anthropic's documentation, so it now applies to whichever platform the user is running.

### Why this matters going forward
This change supports the stated goal of making Sofia usable by any other person, regardless of which AI platform (free or paid) they choose to run her on, without requiring a subscription or platform switch.

---

## Outstanding item (not yet addressed in these versions)

The separate project documentation file (authorship/IP declaration, intended for GitHub/LinkedIn) still references "Sofia runs on claude.ai (Claude by Anthropic)" in its copyright notice and LinkedIn description text. Since Sofia is now platform-agnostic as of v4.2, this document should be updated for consistency between the IP record and the actual system design.

Additionally, the Master Prompt files contain real personal/financial data (investment account figures, a personal email address). If this repository is public, these should be replaced with placeholder values before committing, to avoid exposing personal financial information.
