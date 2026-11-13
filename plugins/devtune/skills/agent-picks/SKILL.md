---
name: agent-picks
description: Use when the user asks which tool or library coding agents (Claude Code, Codex and others) pick or install when asked to add a capability such as auth, payments or email, how often agents pick their product over competitors, why they lose those picks, or to test or re-test agent picks with DevTune.
---

# DevTune Agent Picks

Agent Picks measures which tool a coding agent picks when asked to add a
capability to an app. DevTune runs each request in a fresh test app and records
the packages and code the agent adds. Each scenario is one test app, request,
agent and model. Answer from DevTune tool results, not from general knowledge.

A project can have several setups, one per category or custom job. With more
than one, pass `setup` (its `id` or category slug) on every call; a refusal with
`agent_picks_setup_required` lists them in `details.setups`.

If the Agent Picks tools are refused because the plan lacks Agent Picks, tell
the user it isn't on their DevTune plan.

## Pick the starting read

| The user asks about | Start with |
| --- | --- |
| Pick and install rates from the latest test | `devtune_get_agent_picks_summary` |
| Results by test app, request, agent and model | `devtune_get_agent_picks_cells` |
| Trend across tests | `devtune_get_agent_picks_history` |
| What happened in individual runs | `devtune_list_agent_picks_runs`, then `devtune_get_agent_picks_run_trace` |
| Losing scenarios and what to fix | `devtune_get_agent_picks_actions` |
| A test's status and credits | `devtune_get_agent_picks_test` |
| The schedule | `devtune_get_agent_picks_schedule` |
| Categories, tools, test apps and models to set up | `devtune_get_agent_picks_catalogue` |

Fields, parameters and refusal reasons are in
[Agent Picks API and MCP](https://docs.devtune.ai/agent-picks/api-and-mcp).

## Report picks the way DevTune measures them

- Rates are fractions from 0 to 1: `0.42` is 42%.
- Give every rate with its likely range (`rate_low`, `rate_high`) and its
  coverage. Rates count completed runs only.
- Pick rate and install rate are different numbers. Report both, side by side.
- **Built its own** and **No provider chosen** are outcomes like any tool. Keep
  them in rankings; never fold them into a competitor.
- A `null` rate, `measured: false` or an unfinished test is not measured.
  Report it that way, never as zero.
- When `test.scope` is `public`, the figures come from the category's public
  test, not the user's own.
- Compare two tests only when their `comparison_key` values match, and trends
  only while `judging_key` stays the same.
- A pick records what the agent added. It doesn't prove the integration works
  or explain why the agent chose it. A re-test shows what moved after a fix,
  not that the fix caused it.

## Ask before spending or changing

- Reads are safe to run without asking.
- A paid test, re-test or schedule spends credits. Quote first with
  `devtune_quote_agent_picks_test`, show the user `estimate.high` in credits,
  and start only after they approve, with `max_credits` set to the amount they
  approved. Each start needs a fresh quote; a quote expires after 15 minutes.
- The free starter test can be used once per work domain. Ask before starting
  it.
- Before saving or clearing a setup, changing models, or cancelling a test,
  say what will change and wait for the user to confirm.
- DevTune drafts fixes and never publishes them. Locked pages are off-limits.
- The user's explicit instructions take priority over this skill.
