---
name: deploy-app
description: Deploy anywhere. We currently support your own AWS account and any server you already run (custom VPS). Use when someone wants to connect a cloud account, add a server, connect git, create an app, or deploy.
---

# Deploy an app

CloudPloy runs on the signed-in team's account. Sign-in and cloud authorization happen in the browser. Do not read files from their computer, and do not ask them to paste cloud, git, or payment details into chat.

1. Call `get_account` and `get_limits`. If `can_launch_servers` is false or `note` is set, tell them a team owner can see why in the CloudPloy console, and stop there.
2. For AWS, call `list_provider_credentials` and send its `connect_url` as a link. The CloudPloy connect screen walks them through the AWS steps. When they say they are done, call `list_provider_credentials` again to confirm.
3. Call `estimate_cost` before `provision_server`, with a size from `allowed_sizes` in `get_limits`. For a machine they already have, call `connect_server` instead; its firewall must allow SSH from `ssh_allowed_from`. Then poll `get_server` about every 30 seconds: `setup.current_step` shows the step running now, `status` turns `active` when it is ready (usually 3 to 5 minutes), and `setup.error` says why a launch or connect failed.
4. Call `connect_git_provider` with `github`, `gitlab`, or `bitbucket`. Send `auth_url` as a link. After they finish in the browser, call `list_git_providers`, then `list_git_repositories`.
5. Call `create_app`, then `enable_auto_deploy` if they want pushes to redeploy. Call `deploy_app` for a deploy now. Follow a deploy with `get_deployment` and `get_logs`; `get_runtime_logs` shows what the running app prints, and `get_app` shows its copies after `scale_app`.
6. For a custom domain, call `add_domain` and give them the DNS record in `records`, then call `verify_domain` until it is verified. `set_primary_domain`, `set_domain_redirect` and `remove_domain` change or remove domains. If the team connected Cloudflare, `list_domains` shows each domain's `cdn` (on, off, not_in_cloudflare or unknown); `set_domain_cdn` turns the Cloudflare CDN on or off and `clear_domain_cache` clears its cache for that hostname only (CloudPloy also clears it after each deploy). Remove an app's domains before `delete_app`.

`terminate_server` and `delete_app` are permanent. Call them only when the person asked for that, and pass `confirm=true`. If they didn't confirm, stop and ask.

If a call fails because the server belongs to another team, say so. Don't retry with a different id.

The person is needed for: approving this connection, creating the AWS access key on the connect page, authorizing the Git provider in the browser, and inviting or removing members, changing roles or managing API tokens (a team owner or admin does those in the CloudPloy console; `list_members` gives the link). Everything else you can do yourself.
