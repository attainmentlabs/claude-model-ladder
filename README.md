# Claude Model Ladder

Stop overpaying for AI. One paste makes Claude Code route every task to the cheapest model that can actually do the job, and escalate when a task needs more brainpower.

From the video: [Fable 5 Is Back](https://youtube.com/@MarcusDavidC)

**v2 (July 2026):** now implements both of Anthropic's officially named cost patterns, Orchestrator and Advisor, plus failure-type escalation. Anthropic's own numbers: Orchestrator = 96% of top-model quality at 46% of the cost (BrowseComp); Advisor = about 92% at 63% (SWE-bench Pro).

## What it does

- **Your model picker becomes a mode switch.** Top model session = Orchestrator (it plans, cheap workers execute). Mid model session = Advisor (it executes, and automatically consults the top model at judgment points).
- **Closes the silent quota leak:** every subagent dispatch must name its model explicitly, otherwise it inherits your premium session model and bills at the premium rate.
- **Escalates by failure type:** execution failures step up one tier; judgment failures skip straight to the top model; the upper-mid tier gets one strike before the top model takes over.
- When you run a session on a smaller model, it flags tasks that deserve a stronger model instead of quietly doing a worse job.
- Nothing ships unreviewed: the top model checks subagent output before it lands.

Why it works: benchmarks show the top model on LOW effort beats the mid tier maxed out, and it costs less per finished task because it doesn't retry. Pay for the class, save on the effort.

## Install (60 seconds)

Open Claude Code and paste the contents of [`install-prompt.md`](install-prompt.md). That's it. Claude writes the ladder rules into your own CLAUDE.md, adapted to whatever plan and models you have, and offers to switch on Advisor mode (one settings.json line).

## What's inside

- `install-prompt.md`: the one-paste installer prompt
- `model-ladder-rules.md`: the rules themselves, if you'd rather copy them in by hand

## Who made this

Marcus David. AI news you can verify, playbooks you can copy: [YouTube](https://youtube.com/@MarcusDavidC) · [X](https://x.com/mdavidcyrus)

Maintained by [Attainment](https://attainmentlabs.com), the growth consultancy where we run this ladder in production for client work.
