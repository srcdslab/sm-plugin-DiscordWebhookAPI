<div align="center">
  <h1><code>DiscordWebhookAPI</code></h1>
  <p>
    <strong>Complete wrapper of the Discord Webhook API written in SourcePawn</strong>
  </p>
  <p style="margin-bottom: 0.5ex;">
    <img
        src="https://img.shields.io/github/last-commit/Sarrus1/DiscordWebhookAPI"
    />
    <img
        src="https://img.shields.io/github/issues/Sarrus1/DiscordWebhookAPI"
    />
    <img
        src="https://img.shields.io/github/issues-closed/Sarrus1/DiscordWebhookAPI"
    />
    <img
        src="https://img.shields.io/github/repo-size/Sarrus1/DiscordWebhookAPI"
    />
  </p>
</div>

## Description

An include featuring a well documented, complete wrapper of the Discord Webhook API written in SourcePawn using methodmaps and the [RIPExt extension](https://github.com/ErikMinekus/sm-ripext).

This include's aim is to make it easy for SourceMod developpers to send embeded WebHook messages to Discord servers, with minimal dependencies.

Contrary to other includes, discordWebhookAPI:

- Does not required a separate plugin to run alongside of it.
- Does not rely on SteamWorks or SM-Jansson.
- Is well documented.
- Allows to edit sent webhook messages.
- Provides a comprehensive documentation.
- Uses methodmaps in order to provide support for the Transitional Syntax.

## Requirements

- [RIPExt extension](https://github.com/ErikMinekus/sm-ripext/releases/latest) (included in the repo.)

## How to use the include

1. Download the latest release and drop every file in your `include/` folder.
2. Add `#include <discordWebhookAPI>` to the top of your file.
3. Create your a basic WebHook message using the snippet below.
4. Get a Discord Webhook for your channel by following the tutorial [here](https://www.digitalocean.com/community/tutorials/how-to-use-discord-webhooks-to-get-notifications-for-your-website-status-on-ubuntu-18-04).
5. See a full working example [here](https://github.com/Sarrus1/discordWebhookAPI/blob/master/example.sp).

```cpp
public Action SendDiscordWebhook(int client, int args)
{
	Webhook webhook = new Webhook("This is the content of the webhook.");
	webhook.Execute("https://discord.com/api/webhooks/6758765876/769876789009", OnWebHookExecuted);
	delete webhook;
	return Plugin_Continue;
}

public void OnWebHookExecuted(HTTPResponse response, any data)
{
	// Execute() always appends ?wait=true, so Discord answers 200 OK with the message body.
	if (response.Status == HTTPStatus_OK)
	{
		PrintToServer("Webhook sent successfully!");
	}
}
```

### Discord API version

Webhook URLs copied from Discord are unversioned (`https://discord.com/api/webhooks/...`), which makes Discord fall back to its deprecated default API version.
`Execute()` and `Edit()` therefore pin Discord URLs to API **v10** (`https://discord.com/api/v10/webhooks/...`). URLs that already contain a version, or that do not point to a Discord host, are sent unchanged.

To use another version, define it before the include (`0` disables the rewrite):

```cpp
#define DISCORD_API_VERSION 9
#include <discordWebhookAPI>
```

## Example

![Example-send](https://github.com/Sarrus1/discordWebhookAPI/blob/master/example.png?raw=true)

![Example-edit](https://github.com/Sarrus1/discordWebhookAPI/blob/master/example-2.png?raw=true)
