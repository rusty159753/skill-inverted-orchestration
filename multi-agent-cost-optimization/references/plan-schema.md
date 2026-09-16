# Plan schema

The planner writes this file once, to `./agent-state/plan.md`. The orchestrator reads it
and does not change it. Only the planner changes it, and only after an audit verdict of
correct or escalate.

GOST means Goal, Objectives, Strategy, Tactics.

---

```markdown
# Plan: <run name>

Date: <date>
Tier A model: <name>
Tier B model: <name>

## Goal
<One sentence. The outcome, not the method.>

## Objectives
<Numbered. Each objective is a result, not a task. The human accepted these.>

1. <objective>
2. <objective>

## Strategy
<The approach and the constraints for the whole run. Stable. This is the standard the
auditor checks against. State what the run will do, what it will not do, and the rules
every agent follows.>

Constraints:
- <constraint>
- <constraint>

## Milestones and acceptance criteria

### Milestone 1: <name>
Objective: <number>
Acceptance criteria:
- [ ] <criterion verifiable by reading a named artifact>
- [ ] <criterion verifiable by reading a named artifact>

### Milestone 2: <name>
...

## Tactics for objective 1
<A worked example only. The orchestrator sets tactics for every later objective.>

1. <task>
2. <task>

## Call budget
Expected Tier A calls: <number>
Basis: <how the number was derived, such as tasks per milestone times milestones, plus
one audit per milestone>
Audit at: <50 percent of the number>
Escalate at: <the number>
```

---

## Rules

- Every acceptance criterion names the artifact that proves it. A criterion that cannot be
  checked by reading something is not a criterion.
- Objectives are results. Tactics are tasks. Do not mix them.
- The call budget is a count of Tier A turns, not a token count and not a dollar amount. A
  count is visible in every harness and can be tracked by the orchestrator.
- If the run is a repeat of an earlier run, carry the earlier `failed-approaches.md`
  forward. It is the cheapest control against repeat dead ends.
