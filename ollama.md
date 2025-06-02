### To run language models, you need the `ollama` tool
### Direct installation
```
curl -fsSL https://ollama.com/install.sh | sh
ollama serve
ollama run gemma3:12b
```
### ِDocker installation
```
docker pull ollama/ollama
```
### compose file
```
version: '3.8'

services:
  ollama:
    image: ollama/ollama
    container_name: ollama
    ports:
      - "11434:11434"
    environment:
      - OLLAMA_NO_CUDA=1
    volumes:
      - ollama_data:/root/.ollama
    restart: unless-stopped

volumes:
  ollama_data:
```
### If the server does not have a GPU, we must apply this configuration to use the CPU
```
OLLAMA_NO_CUDA=1
```
### Installing the language model
```
docker exec -it ollama bash
ollama run gemma3
```
### Using API for chat
```
curl http://server-ip:11434/api/generate -s -d '{
                                       "model": "gemma3",
                                       "prompt": "CHAT",
                                       "stream": false
                                     }' | jq -r .response

```
### Functional models
```
ref https://ollama.com/library

openhermes
mistral
deepseek-coder
```
### Functional commands
```
ollama --help
ollama list
ollama stop
ollama run
```
