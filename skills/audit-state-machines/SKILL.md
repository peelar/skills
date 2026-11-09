---
name: audit-state-machines
description: Find the implicit state machines in a codebase, chart each with the statechart skill, and rank them by severity and cleanup.
disable-model-invocation: true
---

# Audit state machines

An implicit state machine is a lifecycle the code never names. Its state hides in **fragments** (flags, nullable fields, timestamps, which record exists, sibling `useState` calls). **Writers** change the fragments, and **guards** re-derive the state from them by hand. Every claim in the audit carries a `file:line`.

1. **Hunt.** Run every search in [`signals.md`](signals.md) over the scope. Mark each candidate **frontend** (its state dies with the session), **backend** (it outlives a request) or **split** (a page that mirrors a backend record). Done when every hit is a candidate or ruled out.
2. **Reconstruct.** For each candidate, list every fragment, and every writer and guard of each fragment. Search the whole scope, including jobs, webhooks, migrations and the other side of the stack. Done when no fragment has a writer you have not listed.
3. **Chart.** Model each machine in TLA+ and draw it with the statechart skill: read `~/.claude/skills/statechart/SKILL.md` and follow it. Write each rule the product means as an INVARIANT, including every combination of fragments that should be impossible and what each guard assumes. A broken rule is a finding, and its path is the repro. Model a split machine as one spec with a region for each side.
4. **Find consequences.** Check each machine for divergent guards, writers that skip the state check, races between requests or instances, dead ends, and terminal states that keep data forever. Confirm each finding with a failing test or a step-by-step `file:line` trace, and mark it CONFIRMED or PLAUSIBLE.
5. **Score.** A machine's severity is that of its worst finding:
   - **Critical:** security, data exposure, or data loss.
   - **High:** a wrong or stuck result on a common path, or secrets kept forever.
   - **Medium:** an impossible state or race on a rare path.
   - **Low:** no finding; the machine is only hard to read.

   Its cleanup is: guards that collapse into one check, impossible states removed (representable combinations minus valid states), files touched, and effort (S, M or L).
6. **Report.** One section per machine, ranked by severity and then cleanup:
   - side and severity;
   - a fragments table: fragment, `file:line`, and the state or transition it encodes;
   - the chart, with its broken rules;
   - the findings;
   - a snippet of the explicit machine, 15 lines at most, in the repo's style: a tagged union and `transition()` for the backend, a reducer over a discriminated union for the frontend;
   - the cleanup numbers.

   End with the three machines to fix first, and why.
