# Claude Model Ladder

Stop overpaying for AI. One paste makes Claude Code route every task to the cheapest model that can actually do the job, and escalate when a task needs more brainpower.

From the video: [Fable 5 Is Back](https://youtube.com/@MarcusDavidC)

## What it does

- Your top model (Fable 5 or Opus 4.8) keeps the thinking work: planning, architecture, judgment calls, final review.
- Mechanical work (running tests, batch edits, data pulls, research sweeps) gets delegated to cheaper subagents (Sonnet, Haiku) automatically.
- When you run a session on a smaller model, it flags tasks that deserve a stronger model instead of quietly doing a worse job.
- Nothing ships unreviewed: the top model checks subagent output before it lands.

Why it works: benchmarks show the top model on LOW effort beats the mid tier maxed out, and it costs less per finished task because it doesn't retry. Pay for the class, save on the effort.

## Install (60 seconds)

Open Claude Code and paste the contents of [`install-prompt.md`](install-prompt.md). That's it. Claude writes the ladder rules into your own CLAUDE.md, adapted to whatever plan and models you have.

## What's inside

- `install-prompt.md` — the one-paste installer prompt
- `model-ladder-rules.md` — the rules themselves, if you'd rather copy them in by hand

## Who made this

Marcus David. AI news and playbooks backed by evidence instead of panic: [YouTube](https://youtube.com/@MarcusDavidC) · [X](https://x.com/mdavidcyrus)

Maintained by [Attainment](https://attainmentlabs.com), the growth consultancy where we run this ladder in production for client work.
