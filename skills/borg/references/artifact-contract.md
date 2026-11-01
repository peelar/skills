# Generated artifacts

Create exactly these two required artifacts. Keep the profile independent of this meta skill.

```text
borg-<login>-review/
  SKILL.md
  references/preferences.md
```

## Person skill

Use this structure, substituting the canonical login and adjusting prose only when needed for the actual evidence. A skill name must match its directory.

```markdown
---
name: borg-<login>-review
description: Review a change through GitHub user <login>'s documented engineering preferences, or discuss a design using their evidence-backed developer profile. Use when the user requests <login>'s likely feedback or invokes this profile.
---

# <login>'s engineering preferences

Read all of [references/preferences.md](references/preferences.md) before reviewing or discussing anything. It contains the profile's scope, limitations, preference states, and evidence. This is an inference from recorded activity, not the person's actual response or endorsement. Give that framing briefly at the start of a session; mention provisional or partial coverage when it affects the answer.

## Review a change

Resolve the requested PR, diff, commit range, or local changes. Read applicable repository instructions and enough surrounding code to assess each relevant preference. If the review target cannot be resolved, ask for it.

Apply each supported preference whose recorded scope matches the change. For every predicted concern, provide:

- The concrete file/line or diff location and the observed issue.
- Why this person may raise it, citing a preference ID and its source link.
- A practical change or question that would address the concern.

Rank concerns by impact. Separate code severity from how confidently the profile predicts the person's reaction; label a stylistic preference as such. Match predicted insistence to evidence of insistence. Present tentative preferences as questions, contested ones with their competing evidence, and exclude superseded preferences from current expectations.

Keep general correctness findings distinguishable from person-specific predictions. Explain material applicability gaps and areas where the change already matches supported preferences. If no preference supports a concern, say so instead of manufacturing feedback. Do not infer approval from silence or impersonate the person's voice. Return feedback in the conversation; posting it to GitHub requires an explicit request.

## Discuss a design

Use the complete log to explain likely tradeoffs, alternatives, and conditions that would change the recommendation. Cite the relevant preference IDs and evidence. Identify unknowns when the profile cannot support an answer. Describe probable reasoning in your own voice.

## Refresh

When asked to refresh the profile, use Borg if available, or explain that the collection workflow is needed. Ordinary reviews and conversations do not silently rewrite the evidence log.
```

## Preference log

Use compact ADR-style entries: context, inferred decision, consequences, and evidence. These are inferred preferences, not decisions authored by the person. Keep descriptions concrete enough to apply to a future change.

Start `references/preferences.md` with:

- **Identity:** canonical GitHub login and profile URL.
- **Coverage:** collection/update dates, requested and actual activity window, repositories, discovery queries, inspected PR URLs, and inspected counts for authored PRs, submitted reviews, inline comments, and general comments. Counts may overlap; count PRs distinctly for independence.
- **Limitations:** actual stopping reason, any explicit budget or operational limit, missing activity types, inaccessible or truncated sources, repository bias, and whether the profile is provisional. When stopping for diminishing returns, describe what recent batches added or confirmed. List unresolved topics rather than assuming preferences for them.
- **Attention:** observed recurring review topics, with entry IDs. Record explicit evidence of limited review scope if present; otherwise skimming behavior remains unknown.
- **Index:** ID, title, state, applicability, last evidence date. Keep the detailed entries below it in the same file so loading the whole log is straightforward.

Each entry uses this schema; substitute actual evidence and omit empty optional content:

```markdown
## P001 — <actionable preference>

- State: supported | tentative | contested | superseded
- Scope: <repository/language/situation and exclusions established by evidence>
- Observed: <first and last evidence dates>; assessed <date>

**Context:** <the recurring problem or tradeoff>

**Inferred decision:** <what this developer tends to prefer under these conditions>

**Consequences:** <benefit they prioritize and cost they accept; distinguish stated reasons from inference>

**Review application:** <concrete trigger to inspect, likely feedback, and observed strength: blocking/request/suggestion/question/unknown>

**Evidence:**
- <date> — [exact comment/review permalink](URL), on [owner/repo#number](URL), authored by <login>. <Faithful paraphrase, context, and thread outcome.>
- <date> — [independent evidence](URL), on [different PR](URL). <What corroborates the same preference.>

**Counterevidence and uncertainty:** <contrary examples with links, plausible scope distinctions, or “none found in the inspected corpus”; attribution limits>

**History:** <dated state/scope changes and reasons; successor/predecessor IDs if applicable>
```

For implementation evidence, link the PR and relevant immutable commit/file when available; establish authorship and explain why the choice appears voluntary. For comments, prefer exact comment anchors over a PR landing page. Paraphrase sources faithfully and keep any quotations short. Never invent a link or claim to have inspected an inaccessible source.

Preserve one entry per distinct preference. Merge duplicates while retaining old IDs as aliases. Separate conditions within an entry when they explain apparent conflict; retain unresolved conflict explicitly. A source withdrawn or unavailable on refresh remains historical evidence marked as unverifiable, rather than silently disappearing.
