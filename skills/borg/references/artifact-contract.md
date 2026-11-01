# Output contract

Three required files; generated profiles must work without Borg:

```text
borg-<login>-review/
  SKILL.md
  references/preferences.md
  references/coverage.json
```

## Generated SKILL.md

Substitute the lowercase canonical login in the name/directory; preserve display spelling in prose. Derive all findings from the log and keep the summary and map synchronized with it.

| Part | Format and purpose |
| --- | --- |
| Profile summary | 2–3 short paragraphs, roughly 180–250 words. Explain how the strongest priorities connect, what tradeoffs the person accepts, and how they respond to feedback. Use entry IDs for attribution. |
| Findings map | One compact row per major current finding, with scope, state, and a link to its log entry. Include important tentative/contested findings; exclude superseded ones. |
| Scope line | Repositories, dates, state counts, and material unknowns. |

The summary should add reasoning and nuance beyond the map. Keep detailed examples, lifecycle narratives, and per-preference explanations in the log. Avoid a paragraph for every finding; greater research depth should improve the synthesis rather than lengthen it.

```markdown
---
name: borg-<login>-review
description: Review a change through GitHub user <login>'s documented engineering preferences, or discuss a design using their evidence-backed developer profile. Use when the user requests <login>'s likely feedback or invokes this profile.
---

# <login>'s engineering preferences

## Profile summary

<Paragraph 1: connect the strongest demonstrated priorities and explain their practical effect. Cite entry IDs.>

<Paragraph 2: explain accepted tradeoffs and contextual exceptions. Cite entry IDs.>

<Optional paragraph 3: describe observed communication and response to feedback. Cite entry IDs.>

**Scope:** <repositories; dates; state counts; material unknowns>.

## Findings map

| Theme | Inferred preference or pattern | When it matters / scope | State | Evidence |
| --- | --- | --- | --- | --- |
| <theme> | <concrete finding> | <trigger and applicability> | <state> | [P001](references/preferences.md#p001) |

<Repeat for the most important findings; order by significance.>

## Use this profile

Read all of [references/preferences.md](references/preferences.md) before review or discussion. Frame predictions as inferences from recorded activity, not actual responses or endorsement. Surface provisional/partial coverage when relevant. Use your own voice.

## Review

Resolve the PR, diff, commit range, or local changes; ask if missing. Read repository instructions and relevant surrounding code. Apply supported preferences within their recorded scope.

For each predicted concern, provide:

- File/line or diff location and concrete issue.
- Likely reaction, preference ID, and original evidence link.
- Practical change or question.

Rank by impact; distinguish code severity from prediction confidence and label style preferences. Match predicted insistence to observed insistence. Tentative findings become questions; contested findings include competing evidence; superseded findings do not define current expectations.

Distinguish general correctness findings from profile predictions. Mention relevant matches and applicability gaps. If evidence supports no concern, say so. Silence does not predict approval. Return feedback here; posting to GitHub requires an explicit request.

## Discussion

Use the complete log to explain likely priorities, communication, tradeoffs, alternatives, and conditions that change the recommendation. Cite IDs and evidence; identify unsupported questions as unknown.

## Refresh

Refresh only when requested, using Borg if available. Otherwise explain that evidence collection is needed. Ordinary review/discussion does not rewrite the log.
```

## references/preferences.md

| Section | Required content |
| --- | --- |
| Identity | Canonical login, profile URL. |
| Coverage | Brief scope and aggregate discovered/inspected counts; link to `coverage.json`. Counts may overlap. |
| Limitations | Stopping reason; budgets/operational limits; inaccessible/truncated sources; missing activity types; repository bias; provisional/partial status. For diminishing returns, state what recent batches added/confirmed. |
| Synthesis | Priorities, tradeoffs, communication patterns, observed review attention, meaningful lifecycle patterns; link entry IDs. Unknowns remain explicit. |
| Index | ID, title, state, scope, last evidence date. Detailed entries follow in this file. |

Keep PR/issue inventories and per-item inspection metadata exclusively in `coverage.json`. Preference entries still cite the original evidence supporting each claim.

### Entry schema

Compact ADR-style entries; one per distinct actionable finding. These are inferred preferences, not decisions authored by the person. Use stable lowercase ID anchors (`p001`, etc.) for map links. Omit empty optional fields.

```markdown
<a id="p001"></a>

## P001 — <actionable preference>

- State: supported | tentative | contested | superseded
- Scope: <repository/language/role/situation; known exclusions>
- Observed: <first–last evidence dates>; assessed <date>

**Context:** <problem or tradeoff>
**Inferred decision:** <preferred choice or observable communication pattern>
**Consequences:** <prioritized benefit; accepted cost; stated rationale vs inference>
**Application:** <review/discussion trigger; likely feedback; observed strength: blocking/request/suggestion/question/unknown>

**Evidence:**
- <date> — [exact source](URL), on [PR/issue](URL), by <login>. <Context → action/response → outcome; what it supports.>
- <date> — [independent source](URL), on [PR/issue](URL). <Corroboration; explain independence if linked.>

**Counterevidence/uncertainty:** <contrary sources, scope distinctions, attribution limits, or “none found in inspected corpus”>
**History:** <dated state/scope changes; predecessor/successor IDs>
```

### Evidence and maintenance

- **Supported:** ≥2 independent PRs/issues; linked items from one decision count as one episode. Tentative evidence can produce a provisional profile.
- Comments/reviews: exact permalink. Code: PR plus immutable commit/file where available; verify authorship and voluntary choice. Lifecycle: event, discussion, and linked outcome; do not assume motive from status alone.
- Paraphrase faithfully; keep quotations short. No invented links or claims of inspecting inaccessible sources.
- Merge duplicates; retain old IDs as aliases. Keep contextual differences within entries; preserve unresolved conflict.
- Refresh preserves sources and dated history. Mark withdrawn/unavailable evidence unverifiable. Keep unsupported user corrections separate from demonstrated preferences.

## references/coverage.json

Collection audit metadata; ordinary review/discussion need not load it.

| Content | Required fields |
| --- | --- |
| Scope | Collection/update dates, requested/actual date window, repositories, discovery queries, pagination/access gaps. |
| Counts | Discovered, retrieved, and inspected counts by activity type; distinguish screening from contextual examination. |
| Inventories | PRs and issues: URL, author, title, lifecycle status/dates where known, inspection depth, and relevant outcome notes. Preserve existing records on refresh. |

Keep inventories out of `SKILL.md` and `preferences.md`; link to this file when needed. Preserve existing JSON structure where practical.
