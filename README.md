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
