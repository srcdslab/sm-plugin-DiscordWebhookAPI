# discordWebhookAPI

![Downloads](https://img.shields.io/github/downloads/Sarrus1/discordWebhookAPI/total) ![Last commit](https://img.shields.io/github/last-commit/Sarrus1/discordWebhookAPI) ![Open issues](https://img.shields.io/github/issues/Sarrus1/discordWebhookAPI) ![Closed issues](https://img.shields.io/github/issues-closed/Sarrus1/discordWebhookAPI) ![Size](https://img.shields.io/github/repo-size/Sarrus1/discordWebhookAPI) ![GitHub Workflow Status](https://img.shields.io/github/workflow/status/Sarrus1/discordWebhookAPI/Compile%20with%20SourceMod)

## Description

An include featuring a well documented, complete wrapper of the Discord Webhook API written in SourcePawn using methodmaps and the [RIPExt extension](https://github.com/ErikMinekus/sm-ripext).

This include's aim is to make it easy for SourceMod developpers to send embeded WebHook messages to Discord servers, with minimal dependencies.

Contrary to other includes, discordWebhookAPI:
- Does not required a separate plugin to run alongside of it.
- Does not rely on SteamWorks or SM-Jansson.
- Is well documented.
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
	webhook.Execute("https://discordapp.com/api/webhooks/6758765876/769876789009/", OnWebHookExecuted);
	return Plugin_Continue;
}

public void OnWebHookExecuted(HTTPResponse response, DataPack pack)
{
	if (response.Status == HTTPStatus_NoContent)
	{
		PrintToServer("Webhook sent successfully!");
	}
}
```

## Example

![Example](https://github.com/Sarrus1/discordWebhookAPI/blob/master/example.png?raw=true)
