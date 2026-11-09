# Skills

My collection of agent skills.

## [Borg](skills/borg/SKILL.md)

Ever wondered what a particular developer would say about your PR?

Borg studies their GitHub PRs, reviews, comments, and issues to learn what they care about and how they give feedback. It creates a skill that mimics their review style, grounded in examples of their actual work.

```text
$borg octocat owner/repo
```

Then use the generated skill to preview their likely feedback:

```text
$borg-octocat-review Review my changes
```

You can also discuss a design through their perspective. Each profile includes a preference log with links to the original evidence—it's an informed prediction, not their actual review.

## [Audit state machines](skills/audit-state-machines/SKILL.md)

Finds the lifecycles a codebase never names: state spread across flags, nullable timestamps, locks, record presence and sibling `useState` calls, with every write and check scattered around it.

For each one, it assembles the pieces into a state machine and charts it with the statechart skill, checking the product's rules against the model. It confirms the bugs this causes and sketches the explicit machine in a short snippet. Machines are split into frontend, backend and split (a page that mirrors a backend record), then ranked by severity and by how much making them explicit cleans up.

```text
/audit-state-machines apps/api
```
