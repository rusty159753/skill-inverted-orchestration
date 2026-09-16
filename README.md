# Inverted Orchestration Skill

`multi-agent-cost-optimization`: a model-agnostic skill for long multi-agent builds.

A long-context, lower-cost model (Tier B) owns the accumulating state. The
highest-capability model (Tier A) works only in short, clean windows to plan, execute
bounded tasks, and audit. Token cost grows with run length, not task difficulty, so the
long history stays on the cheaper model.

## Layout

```
multi-agent-cost-optimization/     the skill (install this folder)
  SKILL.md                         gate, roles, stop conditions (Agent Skills frontmatter)
  AGENTS.md                        full operating procedure, single source of truth
  references/
    plan-schema.md                 planner output format
    state-schema.md                ./agent-state/ files, index, sub-agent contract
docs/
  PRD-multi-agent-cost-optimization.md
```

`SKILL.md` uses the open Agent Skills format. `AGENTS.md` is plain markdown that any LLM
can follow with no harness support. No scripts, no dependencies.

## Install

Clone once:

```bash
git clone https://github.com/rusty159753/skill-inverted-orchestration.git
```

**Claude Code / Codex / other Agent Skills harnesses.** Link or copy the skill folder into
the harness skills directory, e.g. `~/.claude/skills/multi-agent-cost-optimization` or
`~/.agents/skills/multi-agent-cost-optimization`. A link means `git pull` updates the
installed skill.

**Claude Desktop Cowork / claude.ai.** Build the package and upload it in the
Skills section of Claude settings (claude.ai or Desktop); it syncs to Cowork:

```bash
python -m zipfile -c multi-agent-cost-optimization.skill multi-agent-cost-optimization/
```

Re-upload after each change. Tagged releases on GitHub carry a prebuilt `.skill`.

**Any other LLM.** Give the agent `AGENTS.md` and the `references/` folder, and tell it to
read `AGENTS.md` before step 1.

## Updating

Edit files in `multi-agent-cost-optimization/`, bump the date in the SKILL.md
"Assumption of record" if the pricing premise was re-checked, commit, and tag a release.
