# LLm services

Here you can find how to setup and run the LLm services.

- Ollama
- Open WebUI
- OpenAI API

```text
OpenAI API <-> Ollama <-> Open WebUI
```

Example evnironment:

- WLS2 on Windows 10

## [Ollama](https://ollama.com/)

Download the Ollama from [here](https://ollama.com/download).

- Choose the OS you are using. (For example, Linux)
- Start the Ollama by running the following command in the terminal.

    ```bash
    # Open one terminal to run the Ollama server (port 11434)
    ollama serve
    ```

    ```bash
    # Open another terminal to run the Ollama client
    ollama run llama3:8B
    ```

- Other model libraries can be found [here](https://ollama.com/library)

### Installation Ollama with Docker

On Linux, you can run the Ollama with Docker with Nvidia GPU support.

- Install the Nvidia container toolkit.
- Run Ollama inside a Docker container.

    ```bash
    docker run -d --gpus=all -v ollama:/root/.ollama -p 11434:11434 --name ollama ollama/ollama
    ```

- Run a model

    ```bash
    docker exec -it ollama ollama run llama3:8B
    ```

## [Open WebUI](https://github.com/open-webui/open-webui)

Open WebUI is a web interface for the Ollama. It is a web application that can be run on a web browser.

- If Ollama is on your computer, use this command:

    ```bash
    docker run -d -p 3000:8080 --add-host=host.docker.internal:host-gateway -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main
    ```

    If you ``didn't install the Docker``, you can see [here](https://github.com/DanielHo-BS/cheat-sheet/tree/master/Docker) how to install it.

- Open the web browser and go to `http://localhost:3000`
- If you using VScode, you need open a port to `127.0.0.1:3000`

## [AnythingLLN](https://useanything.com/)

AnythingLLM: The all-in-one AI app you were looking for.
Chat with your docs, use AI Agents, hyper-configurable, multi-user, & no fustrating set up required.

### Installation AnythingLLN with Docker

``Tip``

- ``Docker`` installed on your computer.
- ``yarn`` and ``node`` on your computer.
- access to an LLM running locally or remotely.

```bash
docker pull mintplexlabs/anythingllm

export STORAGE_LOCATION=$HOME/anythingllm && \
mkdir -p $STORAGE_LOCATION && \
touch "$STORAGE_LOCATION/.env" && \
docker run -d -p 3001:3001 \
--cap-add SYS_ADMIN \
-v ${STORAGE_LOCATION}:/app/server/storage \
-v ${STORAGE_LOCATION}/.env:/app/server/.env \
-e STORAGE_DIR="/app/server/storage" \
--add-host=host.docker.internal:host-gateway \
mintplexlabs/anythingllm
```

- Open the web browser and go to `http://localhost:3001`

## Using Docker Compose

You can use the `docker-compose.yml` file to run the services.

services:

- Ollama
- Open WebUI
- AnythingLLN

```bash
docker-compose up -d
```
