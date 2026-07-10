# Model Delegation Ladder v2

Copy this section into your global CLAUDE.md (usually `~/.claude/CLAUDE.md`).

Ladder, strongest to cheapest: Fable 5 -> Opus 4.8 -> Sonnet 5 -> Haiku 4.5 (use whichever tiers your plan has).

Anthropic now officially names the two patterns this ladder implements: **Orchestrator** (top model plans, cheap models execute) and **Advisor** (cheap model executes, top model advises on judgment calls). Their published numbers: Orchestrator scored 96% of top-model quality at 46% of the cost (BrowseComp), and Advisor scored about 92% at 63% (SWE-bench Pro). This file wires both into Claude Code.

## Pick your mode with the model picker

Your session model IS the mode switch. Nothing else to configure per session.

- **Top model session (Fable 5) = Orchestrator mode.** You pay premium for planning and judgment; workers stay cheap. Best for architecture and strategy days.
- **Mid model session (Sonnet 5) = Advisor mode, light.** Cheapest. The session executes everything and automatically consults the top model at judgment points. Best for volume execution days.
- **Upper-mid session (Opus 4.8) = Advisor mode, heavy.** Same pattern, stronger executor. Best when the day's work is mostly hard execution and a mid model would escalate constantly.

## The rules

1. **Every subagent dispatch carries an explicit `model` parameter.** An omitted parameter silently inherits the session model and bills the whole subagent at the premium rate. This is the single biggest quota leak the orchestrator pattern closes. Default: Sonnet-tier.

2. The top model keeps: planning, architecture decisions, judgment calls, taste, public-facing copy, and final review of all subagent output before anything ships.

3. **Route taste and strategy to the top model proactively, not reactively.** Public-facing copy, brand voice, design direction, naming, business strategy, positioning, and "what should we do here" calls all get the top model involved before drafting on a mid-tier session, via the advisor tool or a direct dispatch, not after a mid-tier attempt fails review. Don't wait for the stumble when the task is recognizably strategy or taste from the start.

4. Delegate by default: mechanical code execution from a clear spec, writing and running tests, QA sweeps, data pulls, file operations, batch transforms, research fan-outs, summarization. Sonnet-tier is standard execution. Haiku-tier only if your plan has it and only for narrow, well-scoped mechanical sweeps with clear success criteria.

5. **Upper-mid tier (Opus 4.8) is a direct-dispatch option for known-hard subtasks** (complex multi-file implementation, nuanced drafting, adversarial verify passes). When a task is clearly above Sonnet's grade upfront, dispatch it there directly instead of watching Sonnet fail twice first.

6. **Escalate by failure type, not a fixed sequence.** A struggling subagent (2+ failed attempts, circling, failing review twice) escalates automatically: execution-shaped failures (complex code, long synthesis, tricky debugging) go one tier up first, then the top model; judgment-shaped failures (misread intent, architecture calls, taste, ambiguity) skip the middle and go straight to the top model. The upper-mid tier gets ONE strike: if it fails a task once, hand it to the top model. A same-tier retry rarely changes the outcome.

7. When running as a smaller model and a task clearly needs stronger judgment, say so and recommend escalating. Do not quietly produce a worse answer.

8. Never ship unreviewed: the strongest model in the session verifies subagent output before it is committed, merged, or published.

9. Match effort to the task, not to anxiety: coding runs fine at Low or Medium effort on a top-class model; save High and Max for judgment-heavy work. Escalating the model tier does NOT auto-raise effort; they are independent dials.

## Enable Advisor mode (one line of config)

Add to `~/.claude/settings.json` at the top level:

```json
"advisorModel": "claude-fable-5"
```

Set it to the strongest model on your plan.

Some builds also need the opt-in flag in the same file's `env` block:

```json
"CLAUDE_CODE_ENABLE_EXPERIMENTAL_ADVISOR_TOOL": "1"
```

That's it. On any session running a model below the advisor, the executor automatically consults the advisor model when it hits a genuine judgment call (about once per task in Anthropic's testing). In the terminal CLI you can also trigger it manually with `/advisor`.
