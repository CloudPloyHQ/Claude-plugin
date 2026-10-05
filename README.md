# CloudPloy/Claude-plugin

Connect AWS, Google Cloud, a VPS, or another cloud account, and put Cloudflare in front of it, from Claude or Claude Code. The agent talks to `https://app.cloudploy.com/mcp`. This repo is the install package. It doesn't run a second server.

ChatGPT and Codex use [CloudPloy/ChatGPT-plugin](https://github.com/CloudPloyHQ/ChatGPT-plugin).

## Install

Search the Claude directory for `CloudPloy/Claude-plugin`, or open https://claude.ai/directory/cloudploy.

Claude Code installs the same plugin with `/plugin`.

To add the server without the plugin:

```bash
claude mcp add --transport http cloudploy https://app.cloudploy.com/mcp
```

The client opens a browser so you can sign in.

## What's in this repo

- `.claude-plugin/plugin.json` and `.mcp.json` are the Claude plugin.
- `skills/deploy-app/SKILL.md` is the deploy sequence.
- `server.json` is the official MCP Registry entry, name `com.cloudploy/cloudploy`.

## Registry

`com.cloudploy/cloudploy` is published. The public proof file is `https://cloudploy.com/.well-known/mcp-registry-auth`.
