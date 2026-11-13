# DevTune plugin for Claude

Connects Claude to your DevTune project through the DevTune MCP server at
`https://devtune.ai/api/mcp`, and adds skills that tell Claude which DevTune
tool answers each question and how to report DevTune's numbers.

## Requirements

- A DevTune account with a project.

## Connect

In Claude Code, install it with:

```text
/plugin install devtune --marketplace devtunehq/claude-plugins
```

Then sign in to DevTune when Claude asks and choose the
project this connection should use, and the scopes it may use. The connection
can do what your DevTune role allows in that project. To switch projects,
reconnect and choose another.

## What it covers

- **Visibility:** brand awareness, citation presence and share of voice, the AI
  responses behind them, competitors, cited sites and content gaps.
- **AI Traffic:** crawls, answer fetches and AI-referred visits, plus 404
  demand.
- **Actions:** the ranked fix queue, briefs, drafts and the site Audit.
- **Results:** before/after measurement for shipped actions.
- **Agent Picks:** which tool coding agents such as Claude Code and Codex pick
  when asked to add a capability like auth, payments or email, how often they
  pick you, and the losing scenarios to fix.
- **Agents:** DevTune's managed agents and Dex, on plans that include them.

Claude asks before calling a tool that changes project data or spends DevTune
credits. Agent Picks, managed agents and Dex depend on your DevTune plan. DevTune never publishes content for you.

## What it sends

The plugin runs no local code. Claude calls the DevTune MCP server over HTTPS
with an OAuth token from your DevTune sign-in, sending the tool arguments for
each call. It sends nothing anywhere else. See the
[DevTune privacy policy](https://devtune.ai/privacy-policy).

## Package layout

- `.claude-plugin/plugin.json`: plugin identity.
- `.mcp.json`: the DevTune MCP server.
- `skills/get-started`: confirms which project is connected and what it can do.
- `skills/devtune`: how to use the DevTune tools and report their numbers.
- `skills/agent-picks`: how to read and run Agent Picks tests.

## Example prompts

- How visible is my product in AI answers this month?
- Which competitors get cited instead of us, and where?
- What should we fix first to improve our AI visibility?
- How often do coding agents pick us in our latest Agent Picks test?

## Support

[devtune.ai/contact](https://devtune.ai/contact)

## License

MIT. See [LICENSE.md](LICENSE.md).
