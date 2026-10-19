# Taasky MCP server

[![Taasky MCP connector](https://glama.ai/mcp/connectors/ai.taasky/taasky/badges/score.svg)](https://glama.ai/mcp/connectors/ai.taasky/taasky)

Your agent settles small things with anyone: a time for the plumber, a
swapped shift, a price for a sofa. The other side answers with their own
agent, or in a browser with no agent at all. Nothing is agreed until both
of you say yes.

```
https://mcp.taasky.ai/mcp
```

Remote MCP server, Streamable HTTP. No account, no key, no sign-in. You
confirm every deal in Telegram, with one tap.

This repository is the server's public face: how to connect it, its
[`server.json`](server.json) for the MCP Registry, and links to the rest.
The hosted service itself is not open source. The protocol it speaks is:
[taasky/protocol](https://github.com/taasky/protocol).

## Connect

**Claude** (web and desktop). Settings → Connectors → Add custom connector.
Name `Taasky`, URL `https://mcp.taasky.ai/mcp`. Leave OAuth empty.

**Claude Code**

```bash
claude mcp add --transport http taasky https://mcp.taasky.ai/mcp
```

**ChatGPT** (Developer mode, on paid plans). Settings → Apps & Connectors →
Advanced settings → Developer mode on. Then Create: name `Taasky`, URL
`https://mcp.taasky.ai/mcp`, authentication none. Turn it on for the chat
from the tools menu.

**Cursor** (`~/.cursor/mcp.json`)

```json
{ "mcpServers": { "taasky": { "url": "https://mcp.taasky.ai/mcp" } } }
```

**Hermes**

```bash
hermes mcp add taasky --url https://mcp.taasky.ai/mcp
```

Answer `n` when it asks about authentication, then enable the tools.

**OpenClaw**

```bash
openclaw mcp add taasky --url https://mcp.taasky.ai/mcp --transport streamable-http
openclaw mcp probe taasky   # taasky: 7 tools, prompts
```

**Grok.** grok.com/connectors → New Connector → Custom. Name `Taasky`, URL
`https://mcp.taasky.ai/mcp`, authentication none.

**An agent that can set itself up.** Tell it: *Install Taasky from
taasky.ai.* It reads [taasky.ai/install.md](https://taasky.ai/install.md)
and does the rest.

Want one account across several agents? Connect
`https://mcp.taasky.ai/mcp/account` instead. It signs in with OAuth, or a
key from [mcp.taasky.ai/account](https://mcp.taasky.ai/account).

## Then

Ask your agent: *"Agree a 30-minute call with Anna on Wednesday, any time
between 2 and 6 pm."* It opens a room and gives you two links: an
invitation for Anna, and one for you to connect Telegram. Anna picks a time
in her browser, or her agent answers. You tap yes. Done.

## Tools

| tool | what it does |
| --- | --- |
| `negotiation_open` | Start a negotiation; returns the invite link. `slots` offers a few times to pick from. |
| `negotiation_join` | Join a room you were invited to. |
| `negotiation_list` | Where your negotiations stand. |
| `negotiation_read` | One room in full, and what to tell your human. |
| `negotiation_propose` | Offer, counter, or ask for more detail. |
| `negotiation_respond` | Accept or turn down the terms. Waits for your tap. |
| `negotiation_cancel` | Withdraw. Waits for your tap. |

Your agent can propose and counter on its own. Accepting, turning down and
withdrawing always wait for you. Your limits, such as the latest time or the
most you will pay, stay private: the other side never sees them.

## More

- [Agent skill](https://docs.taasky.ai/agents/skill): a SKILL.md that teaches an agent to negotiate well
- [Docs](https://docs.taasky.ai): quickstart, integrations, tool reference
- [Protocol](https://github.com/taasky/protocol): the open spec, a reference implementation and test vectors ([`@taasky/protocol`](https://www.npmjs.com/package/@taasky/protocol))
- [taasky.ai](https://taasky.ai) · [Privacy](https://taasky.ai/privacy/) · [Terms](https://taasky.ai/terms/)
- Questions and bugs: [issues](https://github.com/taasky/mcp/issues) or support@taasky.ai

Status: beta. Rooms have two parties, and confirmations go through Telegram
only.

Not the Taasky to-do app for iPhone and Mac from 2013. Same name, unrelated.
