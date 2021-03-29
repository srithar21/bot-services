# OTC-Bot Bot - `otcBotBot`

## How to register the bot in the Bot Framework portal

In order to create a bot you need to first register it in the [Azure portal](https://portal.azure.com/).

1. Choose to *Create a resource*, or alternatively go to an existing *resource group* and click *Add*
2. Search for *Bot channels registration* and then click *Create*
3. Give the bot a handle (ex: `otcBotBot`), choose your subscription and resource group
4. For the messaging endpoint, use this: `https://otcbot.azurewebsites.net/api/messages`
5. Choose to *Auto create Microsoft App ID and Password*
6. Click *Create*
7. Wait for Azure to finish its magic and when done choose to go to resource
8. On the bot page choose *Channels* and choose to add Microsoft Teams as a channel
9. Next, choose the *Settings* and click on *Manage* next to Microsoft App Id
10. In the Bot app portal, generate a new app password and store it securely - you will need them for your `.env` file or add them as application settings for the hosting web site (see below)

## How to configure the bot
1. brew update && brew install azure-cli


The App Id and App Secret, generated during the registration, for the bot are read from the `MICROSOFT_APP_ID` and `MICROSOFT_APP_PASSWORD` environment variables, specified in the `.env` file. These can be configured in the Azure Web App under *Application Settings > App Settings*.


1. .env - comment prod config and uncomment the qa config
2. Copy the /config/manifest-qa.json content and paste to /src/manifest/manifest.json
3. In terminal: `zip -r com.otc.bot.zip .` for local build `gulp ngrok-serve`
4. Next `az webapp config appsettings set --resource-group  OTC-PROJECT-BOT-SERVICES  --name otc-bot-service --settings WEBSITE_RUN_FROM_PACKAGE="1"`
5. Next `az webapp deployment source config-zip --resource-group  OTC-PROJECT-BOT-SERVICES  --name otc-bot-service --src com.otc.bot.zip`
