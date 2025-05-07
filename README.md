[![Latest Release][version-image]][version-url]
[![caddy on DockerHub][dockerhub-image]][dockerhub-url]
[![Docker Build][gh-actions-image]][gh-actions-url]

# smtp-to-telegram

Fork of the `smtp_to_telegram` project with improved support for telegram super groups.

Original project: https://github.com/KostyaEsmukov/smtp_to_telegram

Getting started
Create a new Telegram bot: https://core.telegram.org/bots#creating-a-new-bot.
Open that bot account in the Telegram account that should receive the messages, press /start.
Retrieve a chat id with curl https://api.telegram.org/bot<BOT_TOKEN>/getUpdates.
Repeat steps 2 and 3 for each Telegram account that should receive the messages.
Start a docker container:
```
docker run \
    --name smtp_to_telegram \
    -e ST_TELEGRAM_CHAT_IDS=<CHAT_ID1>,<CHAT_ID2> \
    -e ST_TELEGRAM_BOT_TOKEN=<BOT_TOKEN> \
	-e ST_TELEGRAM_MESSAGETHREAD_IDS=<THREAD_ID> \
    deniom3/smtp_to_telegram:latest
```
Assuming that your Email-sending software is running in docker as well, you can use smtp_to_telegram:2525 as the target SMTP address. No TLS or authentication is required.

The default Telegram message format is:
```
From: {from}\\nTo: {to}\\nSubject: {subject}\\n\\n{body}\\n\\n{attachments_details}
```
A custom format can be specified as well:
```
docker run \
    --name smtp_to_telegram \
    -e ST_TELEGRAM_CHAT_IDS=<CHAT_ID1>,<CHAT_ID2> \
    -e ST_TELEGRAM_BOT_TOKEN=<BOT_TOKEN> \
	-e ST_TELEGRAM_MESSAGETHREAD_IDS=<THREAD_ID>
    -e ST_TELEGRAM_MESSAGE_TEMPLATE="Subject: {subject}\\n\\n{body}" \
    kostyaesmukov/smtp_to_telegram
```
An example of a docker compose file for running with a local build is given in the repository.

[version-image]: https://img.shields.io/github/v/release/Deniom3/smtp_to_telegram?style=for-the-badge
[version-url]: https://github.com/Deniom3/smtp_to_telegram/releases

[gh-actions-image]: https://img.shields.io/github/actions/workflow/status/Deniom3/smtp_to_telegram/push-docker.yml?style=for-the-badge
[gh-actions-url]: [https://github.com/Deniom3/caddy-cloudflare-transform/actions](https://github.com/Deniom3/smtp_to_telegram/actions)

[dockerhub-image]: https://img.shields.io/docker/pulls/deniom3/smtp_to_telegram?label=DockerHub%20Pulls&style=for-the-badge
[dockerhub-url]: https://hub.docker.com/r/deniom3/smtp_to_telegram
