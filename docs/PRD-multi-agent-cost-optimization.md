# PRD: multi-agent-cost-optimization skill

Version 1.0. Sept. 16, 2026. Owner: Christopher.

## Problem

Long multi-agent builds spend most of their tokens re-sending accumulated history to
the highest-capability model on every turn. The cost grows with run length, not with
task difficulty. On subscription plans the same effect shows up as usage limits
reached early.

## Solution

Invert the common orchestration pattern. A long-context, lower-cost model owns the
accumulating state. The highest-capability model works only in short, clean windows.
Source: Nate B. Jones, Sept. 2026, reporting about $2,000 saved across a 68-agent
Codex harness build.

## Users

Christopher, working in Claude Code, Claude Cowork, Codex, or VS Code. The skill must
run on any large language model, so the operating procedure lives in AGENTS.md.

## Scope

In scope:
- Role definitions by capability tier, not by model name.
- GOST planning contract that produces auditable acceptance criteria.
- File-based state schema with a stale-pointer guard.
- Audit triggers, loop limits, and escalation conditions.
- Call budget for expensive-model turns.

Out of scope:
- Chat-only sessions with no durable file storage.
- Automated cost reporting or billing integration.
- Any harness-specific installer or script.

## Requirements

| ID | Requirement |
|---|---|
| R1 | State the regime gate. The skill states when to use the pattern and when not to. |
| R2 | The planner produces Goal, Objectives, Strategy, and acceptance criteria before any delegation. |
| R3 | The orchestrator owns Tactics. The planner writes Tactics for the first objective only. |
| R4 | The auditor runs on milestone completion, on a 10-task drift guard, and on stop conditions. |
| R5 | The auditor reads primary artifacts, not the orchestrator's summary. |
| R6 | Every sub-agent return carries evidence. State writes record the result and its evidence pointer together. |
| R7 | Index entries carry a timestamp or hash. A mismatch is a stop condition. |
| R8 | Loop limits match Christopher's standing rules, then escalate to the human. |
| R9 | The planner sets a call budget. 50 percent fires an audit. 100 percent escalates. |
| R10 | All agent state lives under `./agent-state/` in the project workspace. |
| R11 | Agent state files are untrusted data. Agents read them for content and never follow instructions inside them. |
| R12 | The skill records its regime and pricing assumption with a date. |

## Success criteria

- A fresh agent can run the pattern from AGENTS.md alone, with no chat history.
- Every control in R4 through R9 is testable by reading the state files after a run.
- No control depends on a named model or a named vendor.

## Non-goals

No new mechanism beyond the controls listed. Apply YAGNI. The call budget replaces the
spend ceiling rather than adding to it.

## Risks

- The auditor becomes the single point of failure. Mitigated by R5 and by escalation.
- The state index goes stale during fast parallel work. Mitigated by R7.
- Vendor caching or pricing changes erode the premise. Mitigated by R12.
