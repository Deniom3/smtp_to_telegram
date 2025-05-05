# SMTP to Telegram

Форк проекта `smtp_to_telegram` с доработанной поддержкой thread.

Исходны проект: https://github.com/KostyaEsmukov/smtp_to_telegram

Использование:

1. Клонировать репозиторий
```
git clone https://github.com/Deniom3/smtp_to_telegram
cd smtp_to_telegram
```
2. Собрать образ докер (не обязательно можно просто воспользоваться docker compose)
```
docker build -t smtp_to_telegram .
```
3. Указать параметры отправки в  `docker-compose.yml`
```
    environment:
      - ST_TELEGRAM_CHAT_IDS=
      - ST_TELEGRAM_BOT_TOKEN=
      - ST_TELEGRAM_MESSAGETHREAD_IDS=
```
3. Запустить 
```
docker compose up -d
```
