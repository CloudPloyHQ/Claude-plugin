# CloudPloy

Deploy an app onto a server in your own cloud account from Claude or ChatGPT. The agent talks to `https://app.cloudploy.com/mcp`. This repo is the install package. It doesn't run a second server.

## Install from a directory

After a listing is published, install it from the directory in that app:

- Claude Desktop, Claude.ai, and Claude Code use the same connector.
- Claude Code and Cowork can also install the plugin, which adds the deploy skill.
- ChatGPT and Codex install the plugin from OpenAI's directory.

Until those listings are live, connect the server directly:

```bash
claude mcp add --transport http cloudploy https://app.cloudploy.com/mcp
```

The client opens a browser so you can sign in.

## What's in this repo

- `.claude-plugin/plugin.json` and `.mcp.json` are the Claude plugin.
- `plugin.json` and `mcp.json` are the ChatGPT and Codex package.
- `skills/deploy-app/SKILL.md` is the deploy sequence.
- `server.json` is the official MCP Registry entry, name `com.cloudploy/cloudploy`.

## Package the ChatGPT zip

From this directory:

```bash
zip -r dist/cloudploy-agent.zip \
  plugin.json mcp.json .mcp.json server.json LICENSE README.md \
  .claude-plugin skills assets .codex-plugin
```

Upload that zip in the OpenAI plugin dashboard. Reviewer login stays in the dashboard, not in the zip.

Before you submit, leave reviewer login in the OpenAI dashboard. Record a short demo of the five positive cases and paste that URL into the review form. The test account needs a team that can already deploy, with one server and one app, and sign-in that doesn't use MFA, email codes, or SMS.

Allowed link origins you own: `https://app.cloudploy.com` and `https://cloudploy.com`.

## Registry

`com.cloudploy/cloudploy` is published. The public proof file is `https://cloudploy.com/.well-known/mcp-registry-auth`.

## Hand-in for the directories

Claude, on a paid plan: [claude.ai/directory/manage](https://claude.ai/directory/manage). Submit the MCP connector (`https://app.cloudploy.com/mcp`) and this repo as a plugin bundle. Connect GitHub first. Publish after the scan passes.

OpenAI: verify the business, upload the zip, complete the domain challenge, then submit. Tool changes after launch are a rescan. Skill or copy changes need a new zip.

When a listing URL exists, add it to [cloudploy.com/mcp](https://cloudploy.com/mcp).
