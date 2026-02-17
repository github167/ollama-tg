```
export TG_TOKEN=<tg token>
export CHAT_ID=<chat id>
export MY_OLLAMA_MODEL=${HOME}/model

```



```

docker run -d --rm -v ${MY_OLLAMA_MODEL}:/root/.ollama -p 11434:11434 --name ollama ollama/ollama
#docker exec -it ollama ollama pull qwen2.5:0.5b

```
```
docker run -d --rm \
 --add-host host.docker.internal:host-gateway \
 -e TOKEN=${TG_TOKEN} \
 -e ADMIN_IDS=${CHAT_ID} \
 -e USER_IDS=${CHAT_ID} \
 -e OLLAMA_BASE_URL=host.docker.internal \
 -e INITMODEL=qwen2.5:0.5b \
 rizkypsr/ollama-tg

```
