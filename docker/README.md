1. init environment variables
```
export TG_BOT_TOKEN=<tg bot token>
export CHAT_ID=<chat id>
export MY_OLLAMA_MODEL=${HOME}/model

```
2. start ollama server
```
docker run -d --rm -v ${MY_OLLAMA_MODEL}:/root/.ollama -p 11434:11434 --name ollama ollama/ollama
#docker exec -it ollama ollama pull qwen2.5:0.5b

```
3. start ollama-tg docker image
```
docker run -d --rm \
 --add-host host.docker.internal:host-gateway \
 -e TOKEN=${TG_BOT_TOKEN} \
 -e ADMIN_IDS=${CHAT_ID} \
 -e USER_IDS=${CHAT_ID} \
 -e OLLAMA_BASE_URL=host.docker.internal \
 -e INITMODEL=qwen2.5:0.5b \
 rizkypsr/ollama-tg

```
4. type "/start" in your bot


