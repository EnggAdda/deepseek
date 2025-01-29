# deepseek
#docker-compose
version: '3.8'

services:
  ollama:
    image: ollama/ollama:latest
    container_name: ollama_container
    ports:
      - "11434:11434"
    volumes:
      - ollama_data:/root/.ollama
    restart: unless-stopped

volumes:
  ollama_data:
