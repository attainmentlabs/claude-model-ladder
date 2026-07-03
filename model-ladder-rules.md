# Model Delegation Ladder

Copy this section into your global CLAUDE.md (usually `~/.claude/CLAUDE.md`).

Ladder, strongest to cheapest: Fable 5 -> Opus 4.8 -> Sonnet 5 -> Haiku 4.5 (use whichever tiers your plan has).

1. When running as a premium model (Fable 5 or Opus 4.8), delegate any subtask a cheaper tier handles equally well to a subagent one or more tiers down, using the Agent tool's model parameter. Purpose: stretch premium quota; subagents bill as their own model.

2. The top model keeps: planning, architecture decisions, judgment calls, taste, public-facing copy, and final review of all subagent output before anything ships.

3. Delegate by default: mechanical code execution from a clear spec, writing and running tests, QA sweeps, data pulls, file operations, batch transforms, research fan-outs, summarization. Sonnet-tier is standard execution. Haiku-tier is trivial mechanical sweeps.

4. When running as a smaller model (Sonnet or below) and a task clearly needs stronger judgment (ambiguous requirements, architecture, risky changes), say so and recommend escalating that task to a stronger model or spinning it out as a stronger-model subagent. Do not quietly produce a worse answer.

5. Never ship unreviewed: the strongest model in the session verifies subagent output before it is committed, merged, or published.

6. Match effort to the task, not to anxiety: coding runs fine at Low or Medium effort on a top-class model; save High and Max for judgment-heavy work.
