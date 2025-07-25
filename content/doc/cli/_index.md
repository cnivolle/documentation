---
type: "docs"
weight: 8
title: Clever Tools (CLI)
description: Use Clever Cloud CLI, Clever Tools
aliases:
- /developers/doc/clever-tools/getting_started
- /developers/doc/cli/getting_started
- /doc/administrate/clever-tools/getting_started
- /doc/clever-tools/getting_started
- /doc/cli/getting_started
- /doc/getting-started/cli
- /doc/quickstartcli
- /doc/reference/clever-tools/getting_started
- /doc/reference/clever-tools
---

Clever Tools is the command line interface (CLI) of Clever Cloud. You can use it to create and manage multiple services of the platform as applications, databases or storage add-ons. It also provides easy authenticated access to Clever Cloud public APIv2 and APIv4 through the [`clever curl` command](#curl). It's an [easy to set up](install) multiplatform and open source tool, based on Node.js.

You can contribute to it through [issue](https://github.com/CleverCloud/clever-tools/issues) or [pull requests](https://github.com/CleverCloud/clever-tools/pulls). Ask for new features, enhancements or help us to provide them to our community.

- [How to install Clever Tools](install)
- [Create a Clever Cloud account](https://console.clever-cloud.com)

You'll find below the first commands to know to connect Clever Tools to your account, get its information and manage some options. Others are developed in dedicated pages:

{{< cards >}}
  {{< card link="install" title="Install" icon="arrow-down-tray" >}}
  {{< card link="addons" title="Create and manage add-ons" icon= "wrench-screwdriver" >}}
  {{< card link="applications" title="Create and manage applications" icon="code-bracket" >}}
  {{< card link="kv-stores" title="Manage KV stores" icon="server-stack" >}}
  {{< card link="logs-drains" title="Manage logs, drains" icon="command-line" >}}
  {{< card link="network-groups" title="Network Groups" icon="tcp-ip-service" >}}
  {{< card link="notifications-webhooks" title="Notifications, Web hooks" icon="bell" >}}
  {{< card link="services-depedencies" title="Services dependencies" icon="endpoints" >}}
{{< /cards >}}

## basic commands

To show Clever tools available commands, use:

```
clever
clever help
```

For each of them, you can add these parameters:

```
[--help, -?]            Display help about this program (default: false)
[--version, -V]         Display the version of this program (default: false)
[--color]               Choose whether to print colors or not. You can also use --no-color (default: true)
[--update-notifier]     Choose whether to use update notifier or not. You can also use --no-update-notifier (default: true)
[--verbose, -v]         Verbose output (default: false)
```

> [!TIP]
> For commands returning a list of items, you can use `--format json` or `-F json` to get a JSON output.

## features

Some features are available as experimental, before they're completely ready for prime time. They usually work well, but this testing phase allows us to get feedbacks, refine some details, documentation, and break things between two releases.

Experimental features can be (de)activated on-demand. To list them, use:

```
clever features
```

To (de)activate an experimental feature, use:

```
clever features enable theFeature
clever features disable theFeature
```

To get information about how to use an experimental feature, use:

```
clever features info theFeature
```

## diag | version

To check the current version or get information about your setup, use:

```
clever version
clever diag
clever diag --format json
```

> [!NOTE]
> Such information are nice to provide in your issues report or when you contact Clever Cloud technical support team.

## login | logout

To connect to your Clever Cloud account, use:

```
clever login
```

It will open your default browser and start an Open Authorization ([OAuth](https://en.wikipedia.org/wiki/OAuth)) process to get a `token` and `secret` pair added in your account if it succeeds. You can manage it from the [Console](https://console.clever-cloud.com/users/me/oauth-tokens). Clever Tools will automatically store these `token` and `secret` values in a hidden `clever-tools.json` config file in the current local user home folder.

If you already know them, you can use:

```
clever login --secret SECRET --token TOKEN
```

> [!TIP]
> If environment variables `CLEVER_SECRET` and `CLEVER_TOKEN` are set, Clever Tools will use them, `login` is not needed.

To log out, delete this file or use:

```
clever logout
```

## profile

To get information about the current logged-in user (ID, name, email, 2FA activation, etc.), use:

```
clever profile
clever profile open
clever profile -F json
```

## emails

To list primary email and secondary emails associated with your Clever Cloud account, you can use:

```
clever emails
```

To open the email management page in your browser, use:

```
clever emails open
```

To add a secondary email, use:

```
clever emails add email@example.com
```

To set a secondary email as primary, use:

```
clever emails primary email@example.com
```

To remove one or all secondary emails, use:

```
clever emails remove email@example.com
clever emails remove-all
clever emails remove-all --yes
```

## ssh-keys

To list public SSH keys associated with your Clever Cloud account, you can use:

```
clever ssh-keys
```

To open the public SSH keys management page in your browser, use:

```
clever ssh-keys open
```

To add a new public SSH key, use:

```
clever ssh-keys add myPublicKey ~/.ssh/id_ecdsa.pub
```

To remove one or all public SSH keys, use:

```
clever ssh-keys remove myPublicKey
clever ssh-keys remove-all
clever ssh-keys remove-all --yes
```

## curl

To use our public API, you need to be authenticated for most endpoints. If you're logged in through Clever Tools, there is a simple way to make any request you want: `clever curl`. It's `curl`, but in an authenticated context for Clever Cloud API.

- [Clever Cloud public APIv2 documentation](/developers/api/v2/)
- [Clever Cloud public APIv4 documentation](/developers/api/v4/)

## tokens

You can query [Clever Cloud public API](/developers/api/) with a bearer token thanks to the Auth Bridge. To create a token, use:

```
clever tokens create myTokenName
clever tokens create myTokenName --expiration 2w --format json
```

Once created, you can use it replacing the API endpoint with `https://api-bridge.clever-cloud.com`. For example:

```
curl https://api-bridge.clever-cloud.com/v2/self -H "Authorization: Bearer myToken"
```

To list all your tokens, use:

```
clever tokens
clever tokens -F json
```

To revoke a token, use:

```
clever tokens revoke myTokenId
```
