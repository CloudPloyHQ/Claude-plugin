---
name: deploy-app
description: Deploy anywhere. We currently support AWS, custom VPS, and GCE. More services are coming soon. Use when someone wants to connect a cloud account, add a server, connect git, create an app, or deploy.
---

# Deploy an app

CloudPloy runs on the signed-in team's account. Sign-in and cloud authorization happen in the browser. Do not read files from their computer, and do not ask them to paste cloud, git, or payment details into chat.

1. Call `get_account`. If the team has no usable plan, send them to https://cloudploy.com/pricing and tell them to subscribe in the CloudPloy console. Don't open a checkout from chat.
2. For AWS, call `list_provider_credentials` and send its `connect_url` as a link. The CloudPloy connect screen walks them through the AWS steps. When they say they are done, call `list_provider_credentials` again to confirm.
3. Call `estimate_cost` before `provision_server`. For a machine they already have, call `connect_server` instead. Then poll `get_server`: `setup.current_step` shows the step running now, and `setup.error` says why a launch failed.
4. Call `connect_git_provider` with `github`, `gitlab`, or `bitbucket`. Send `auth_url` as a link. After they finish in the browser, call `list_git_providers`, then `list_git_repositories`.
5. Call `create_app`, then `enable_auto_deploy` if they want pushes to redeploy. Call `deploy_app` for a deploy now.

`terminate_server` and `delete_app` are permanent. Call them only when the person asked for that, and pass `confirm=true`. If they didn't confirm, stop and ask.

If a call fails because the server belongs to another team, say so. Don't retry with a different id.
