# The installer prompt

Paste everything in the block below into Claude Code:

```text
Add a "Model Delegation Ladder" section to my global CLAUDE.md (create the file if it doesn't exist, back it up first if it does). Adapt the model names to the models actually available on my plan. Then offer to enable Advisor mode by adding "advisorModel" (set to the strongest model on my plan) to my ~/.claude/settings.json, plus the env flag CLAUDE_CODE_ENABLE_EXPERIMENTAL_ADVISOR_TOOL=1 if my build needs it. Confirm what you wrote.

The rules to add:

## Model Delegation Ladder

Ladder, strongest to cheapest: Fable 5 -> Opus 4.8 -> Sonnet 5 -> Haiku 4.5 (use whichever tiers my plan has).

Mode is set by my session model picker: top model session = Orchestrator mode (it plans and delegates, workers stay cheap); mid model session = Advisor mode (it executes and consults the top model at judgment points via the advisor tool).

1. Every subagent dispatch must carry an explicit model parameter. An omitted parameter silently inherits the session model and bills the whole subagent at the premium rate. Default: Sonnet-tier.

2. The top model keeps: planning, architecture decisions, judgment calls, taste, public-facing copy, and final review of all subagent output before anything ships.

3. Delegate by default: mechanical code execution from a clear spec, writing and running tests, QA sweeps, data pulls, file operations, batch transforms, research fan-outs, summarization. Sonnet-tier is standard execution. Haiku-tier only for narrow, well-scoped mechanical sweeps with clear success criteria.

4. Upper-mid tier (Opus 4.8) is a direct-dispatch option for known-hard subtasks (complex multi-file implementation, nuanced drafting, adversarial verify passes). When a task is clearly above Sonnet's grade upfront, dispatch it there directly instead of watching Sonnet fail twice first.

5. Escalate by failure type, not a fixed sequence. A struggling subagent (2+ failed attempts, circling, failing review twice) escalates automatically: execution-shaped failures go one tier up first, then the top model; judgment-shaped failures (misread intent, architecture, taste, ambiguity) skip the middle and go straight to the top model. The upper-mid tier gets one strike: if it fails once, hand the task to the top model.

6. When running as a smaller model and a task clearly needs stronger judgment, say so and recommend escalating. Do not quietly produce a worse answer.

7. Never ship unreviewed: the strongest model in the session verifies subagent output before it is committed, merged, or published.

8. Match effort to the task, not to anxiety: coding runs fine at Low or Medium effort on a top-class model; save High and Max for judgment-heavy work. Model tier and effort are independent dials.
```
