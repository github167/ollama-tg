1. init environment variables
```
export TG_BOT_TOKEN="tg bot token"
export CHAT_ID="chat id"
export MY_OLLAMA_MODEL=${HOME}/model

```

2 pull Qwen2.5:0.5b if not pulled yet
```
docker run -d --rm -v ${MY_OLLAMA_MODEL}:/root/.ollama -p 11434:11434 --name ollama ollama/ollama
docker exec -it ollama ollama pull qwen2.5:0.5b
docker exec -it ollama ollama list
docker stop ollama

```
2. clone the repo
```
git clone https://github.com/github167/ollama-tg
cd ollama-tg/docker-compose

cat << EOF > .env
TOKEN=${TG_BOT_TOKEN}
ADMIN_IDS=${CHAT_ID}
USER_IDS=${CHAT_ID}
ALLOW_ALL_USERS_IN_GROUPS=0
INITMODEL=qwen2.5:0.5b
TIMEOUT=3000
OLLAMA_BASE_URL=ollama-server
LOG_LEVEL=DEBUG

EOF

cat << EOF > docker-compose.yml
services:
  ollama-tg:
    build: .
    container_name: ollama-tg
    restart: on-failure
    env_file:
      - ./.env
  ollama-api:
    image: ollama/ollama:latest
    container_name: ollama-server
    volumes:
      - ${MY_OLLAMA_MODEL}:/root/.ollama
    restart: always
    ports:
      - '11434:11434'

EOF

```
2. start all containers
```
docker compose up
#docker compose down

```
3. type "/start" in your bot


