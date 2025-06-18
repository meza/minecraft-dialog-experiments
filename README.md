# Stonecraft-template

Set up a new multi-loader, multi-version mod project with Stonecraft.

- [ ] Update the gradle.properties file with your mod details
- [ ] Update the settings.gradle.kts file with the versions you want to support and the mod name on the bottom
- [ ] Rename the group folders in the src folder to match your mod.group
- [ ] Rename the `yourmodid.accesswidener` file in `src/main/resources` to match your actual mod.id
- [ ] Update the .releaserc.json file's discord notification section with your mod details - or remove the section if you don't want it
- [ ] Check if the java version is what you want it to be in `.github/workflows/build.yml` (`java-version: 21`)
- [ ] Check if you need the datagen step in the `.github/workflows/build.yml` file. If you don't, remove it.
- [ ] If you're not running gametests (which you should), then remove all references to `chiseledGameTest` in the `.github/workflows/build.yml` file
- [ ] Set up the environment variables in GitHub

## Bootstrap with GitHub Actions

The template comes with the `.github/workflows/bootstrap.yml` file that automates the above steps for you.
Just naviate to the Actions tab of your repository and run the `🪄 Initialise Stonecraft template` workflow manually.

## Environment Variables

- `GH_TOKEN` **Secret** - Your Personal GitHub token
- `MODRINTH_ID` **Variable** - Your Modrinth mod ID
- `MODRINTH_TOKEN` **Secret** - Your Modrinth API token
- `CURSEFORGE_ID` **Variable** - Your Curseforge mod ID
- `CURSEFORGE_TOKEN` **Secret** - Your Curseforge API token
- `DISCORD_WEBHOOK` **Secret** - Your Discord webhook URL to use for notifications. This needs to be a bot token, not a user token.

## GitHub Token How-To

This is only needed if you're planning on releasing to Github, which is the default of this template.

1. Go to your [GitHub settings](https://github.com/settings/tokens)
2. Click on `Generate new token`
3. I recommend using a classic token, but make sure to use a new one for each repo. Never reuse tokens to reduce the risk of a token being leaked.
4. Give the token a name that makes sense to you (usually the repo name)
5. Select the `repo` scope and whatever else you need. If you're not sure, just select `repo`.

## Discord Webhook How-To

### Getting a bot token

1. Go to Discord's developer portal https://discord.com/developers/applications
2. Create a new application if you don't have one already
3. Go to the `Bot` section of the application and copy the token and paste it somewhere temporarily (I recommend secure notes in your preferred password manager)

### Setting up the discord server

1. Invite the bot to your server where you want it to post notifications
2. Go to the server settings and create a channel for the bot to post notifications in
3. Go to your personal discord settings and enable developer mode in the Advanced section
4. Right-click the channel you want the bot to post in and click `Copy Channel ID`

### Setting up the webhook

1. Open up Postman or any other tool you're comfortable with to make a POST request
2. Set the URL to `https://discord.com/api/v9/channels/{channel_id}/webhooks`
3. Set the `Authorization` header to `Bot {your_bot_token}`
4. Set the `Content-Type` header to `application/json`
5. Set the body to `{"name": "Your Webhook Name"}`
6. Send the request
7. Copy the webhook URL from the response and paste it into the `DISCORD_WEBHOOK` environment variable
