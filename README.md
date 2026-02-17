Original: https://github.com/rikkichy/ollama-telegram

1. obtain bot token from BotFather
2. send sth to the bot, and execute the following command to find the chat id in key "chat"
https://api.telegram.org/bot<bot_token>/getUpdates

3. example to send
```
export TG_BOT_TOKEN="tg bot token"
export CHAT_ID="chat id"
curl -X POST \
     -H 'Content-Type: application/json' \
     -d '{"chat_id": "${CHAT_ID}", "text": "This is a test from curl", "disable_notification": true}' \
     https://api.telegram.org/bot${TG_BOT_TOKEN}/sendMessage

```
