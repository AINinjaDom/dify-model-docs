# Dify Installation and Setup Documentation

---

This document provides comprehensive instructions for installing and configuring **Dify**, **Ngrok**, **Ollama models**, and custom components (e.g., `flux.1-dev`, `whisper-base`, `piper-tts`) on a **Mac Mini M4 Pro** running **macOS Sequoia**. Tailored for a **multi-agent system**, it supports models like `llava:latest`, `gemma2:latest`, `nomic-embed-text:latest`, `llama3.2:latest`, `qwen2.5:14b`, `mistral:7b`, `phi3:3.8b`, `bge-small-en-v1.5`, `bakllava`, `codellama:7b`, `borch/llama3_speed_chat`, and `wangshenzhi/llama3-8b-chinese-chat`. It covers **installation**, **setup**, **running**, **troubleshooting**, and **organization** for easy reference in Dify’s Knowledge Base or a Git repository.

---

## Table of Contents

- [Prerequisites](#prerequisites)
- [1. Installing Dify](#1-installing-dify)
  - [Steps](#steps-for-dify)
  - [Troubleshooting](#troubleshooting-dify)
- [2. Installing and Setting Up Ngrok](#2-installing-and-setting-up-ngrok)
  - [Steps](#steps-for-ngrok)
  - [Troubleshooting](#troubleshooting-ngrok)
- [3. Installing and Setting Up Ollama Models](#3-installing-and-setting-up-ollama-models)
  - [Ollama Installation](#ollama-installation)
  - [Model Details](#model-details)
- [4. Installing and Setting Up Custom Components](#4-installing-and-setting-up-custom-components)
  - [flux.1-dev (Text-to-Image)](#flux1-dev-text-to-image)
  - [whisper-base (Speech-to-Text)](#whisper-base-speech-to-text)
  - [piper-tts (Text-to-Speech)](#piper-tts-text-to-speech)
- [5. Running All Components](#5-running-all-components)
- [6. Organizing Documentation](#6-organizing-documentation)
- [7. Testing and Validation](#7-testing-and-validation)
- [8. Troubleshooting](#8-troubleshooting)

---

## Prerequisites

Before starting, ensure the following are met:

| Requirement            | Details                                                                 |
|-----------------------|-------------------------------------------------------------------------|
| **Mac Mini M4 Pro**   | 16GB+ RAM, macOS Sequoia, ~50GB free storage.                          |
| **Homebrew**          | Install: `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"` |
| **Git**               | Install: `brew install git`                                            |
| **Python 3.10+**      | Install: `brew install python`                                         |
| **Docker Desktop**    | Download from [docker.com](https://www.docker.com/products/docker-desktop/) and install. Ensure running. |
| **Ngrok Account**     | Sign up at [ngrok.com](https://ngrok.com) for an authtoken.            |
| **Internet Connection** | Required for downloads.                                               |

- **Verify Setup**:
  ```bash
  brew --version
  git --version
  python3 --version
  docker --version
  ```

---

## 1. Installing Dify

Dify is deployed via Docker for streamlined management on your Mac Mini M4 Pro.

### Steps for Dify

1. **Clone Dify Repository**:
   ```bash
   git clone https://github.com/langgenius/dify.git
   cd dify/docker
   ```

2. **Install Docker Dependencies**:
   ```bash
   brew install docker docker-compose
   ```

3. **Start Dify**:
   ```bash
   docker-compose up -d
   ```
   - This launches Dify on **port 3000**.

4. **Verify Installation**:
   - Open a browser and navigate to `http://localhost:3000`.
   - Sign up and log in to the Dify dashboard.
   - Check running containers:
     ```bash
     docker ps
     ```
     - Expected: Containers like `dify-nginx`, `dify-api`, `dify-worker`, `dify-db`.

### Troubleshooting Dify

- **Connection Refused**:
  - Ensure Docker is running and port 3000 is free:
    ```bash
    lsof -i :3000
    sudo kill -9 <PID>
    ```
  - Check logs:
    ```bash
    docker logs dify-nginx-1
    ```

- **PluginDaemonBadRequestError**:
  - Clear duplicate plugins:
    ```bash
    rm -rf ~/dify/docker/plugins/yourusername_plugin-name
    docker exec dify-db-1 psql -U postgres -d dify -c "DELETE FROM plugins;"
    ```
  - Waive signature verification:
    ```bash
    echo "FORCE_VERIFYING_SIGNATURE=false" >> ~/dify/docker/.env
    docker-compose restart
    ```

---

## 2. Installing and Setting Up Ngrok

Ngrok creates a public URL (e.g., `https://abc123.ngrok.io`) to expose your local Dify server (`http://192.168.50.122:3000`) for external access from your phone.

### Steps for Ngrok

1. **Install Ngrok**:
   ```bash
   brew install ngrok/ngrok/ngrok
   ```
   - Verify:
     ```bash
     ngrok version
     ```

2. **Authenticate Ngrok**:
   - Obtain your authtoken from [Ngrok Dashboard](https://dashboard.ngrok.com).
   - Run:
     ```bash
     ngrok config add-authtoken <your-authtoken>
     ```
   - Verify configuration:
     ```bash
     cat ~/.ngrok2/ngrok.yml
     ```
     - Look for `authtoken: <your-authtoken>`.

3. **Run Ngrok**:
   ```bash
   ngrok http 3000
   ```
   - Note the forwarding URL (e.g., `https://abc123.ngrok.io`).

4. **Access Dify Externally**:
   - On your phone (mobile data or different Wi-Fi), open:
     ```text
     https://abc123.ngrok.io/apps
     ```

5. **Stop Ngrok**:
   - Press `Ctrl+C` in the terminal.

### Troubleshooting Ngrok

- **Command Not Found**:
  - Ensure Ngrok is in PATH:
    ```bash
    echo 'export PATH="/usr/local/bin:$PATH"' >> ~/.zshrc
    source ~/.zshrc
    ```

- **Tunnel Limit**:
  - Free Ngrok accounts have session limits. Upgrade for static URLs or use:
    ```bash
    ngrok http --domain=your-dify.ngrok.io 3000
    ```

- **Connection Issues**:
  - Test local Dify:
    ```bash
    curl http://localhost:3000
    ```
  - Check firewall:
    ```bash
    sudo /usr/libexec/ApplicationFirewall/socketfilterfw --add /usr/local/bin/ngrok
    ```

---

## 3. Installing and Setting Up Ollama Models

Ollama hosts AI models for your multi-agent system. Install Ollama first if not done:

```bash
brew install ollama
ollama serve
```

### Ollama Installation

- **Verify**:
  ```bash
  ollama version
  ```
- **Start**:
  ```bash
  ollama serve
  ```
- **Test**:
  ```bash
  curl http://localhost:11434
  ```

### Model Details

Below is a table of installed models, their installation commands, sizes, and use cases:

| Model Name                        | Type         | Size    | Install Command                           | Use Case                     |
|-----------------------------------|--------------|---------|-------------------------------------------|------------------------------|
| `llava:latest`                    | Vision LLM   | ~4.7 GB | `ollama pull llava:latest`                | Image description            |
| `gemma2:latest`                   | LLM          | ~5.4 GB | `ollama pull gemma2:latest`               | Conversational reasoning     |
| `nomic-embed-text:latest`         | Embedding    | ~274 MB | `ollama pull nomic-embed-text:latest`     | Semantic search              |
| `llama3.2:latest`                 | LLM          | ~2.0 GB | `ollama pull llama3.2:latest`             | Function calling             |
| `qwen2.5:14b`                     | LLM          | ~9.0 GB | `ollama pull qwen2.5:14b`                 | Advanced reasoning           |
| `mistral:7b`                      | LLM          | ~4.1 GB | `ollama pull mistral:7b`                  | Task planning                |
| `phi3:3.8b`                       | LLM          | ~2.3 GB | `ollama pull phi3:3.8b`                   | Quick tasks                  |
| `bge-small-en-v1.5`               | Embedding    | ~133 MB | `ollama pull bge-small-en-v1.5`           | Reranking                    |
| `bakllava`                        | Vision LLM   | ~4.5 GB | `ollama pull bakllava`                    | Image analysis               |
| `codellama:7b`                    | Code LLM     | ~3.8 GB | `ollama pull codellama:7b`                | Code generation              |
| `borch/llama3_speed_chat`         | LLM          | ~4.5 GB | `ollama pull borch/llama3_speed_chat`     | Conversational tasks         |
| `wangshenzhi/llama3-8b-chinese-chat` | LLM       | ~4.5 GB | `ollama pull wangshenzhi/llama3-8b-chinese-chat` | Cantonese/Chinese support |

### Setup and Testing
- **For Each Model**:
  - Install with `ollama pull <model-name>`.
  - Test:
    ```bash
    ollama run <model-name> "Hello, test the model."
    ```
    - Example: `ollama run llava:latest "Describe this image."` (with an image).
- **Dify Integration**:
  - Add models in **Settings** > **Model Providers** > **Ollama**.
  - Example settings for `qwen2.5:14b`:
    - Model Type: LLM
    - Model Name: `qwen2.5:14b`
    - Base URL: `http://host.docker.internal:11434`
    - Completion Mode: Chat
    - Model Context Size: 32768
    - Upper Bound for Max Tokens: 4096
    - Vision Support: No
    - Function Call Support: Yes

---

## 4. Installing and Setting Up Custom Components

Custom components (`flux.1-dev`, `whisper-base`, `piper-tts`) are not in Ollama and require Python-based APIs for Dify integration.

### flux.1-dev (Text-to-Image)

- **Purpose**: Generates images from text prompts.
- **Size**: ~12 GB
- **Install Dependencies**:
  ```bash
  pip install torch torchvision torchaudio diffusers transformers accelerate fastapi uvicorn
  ```
- **Setup Script**:
  - Create `flux_api.py`:
    ```python
    # artifact_id: 3b8e5c1d-7f2a-4c9b-9e8f-6a2b3d4e5f6b
    # title: flux_api.py
    # contentType: text/python
    from fastapi import FastAPI
    from diffusers import FluxPipeline
    import torch
    from fastapi.responses import JSONResponse
    import base64
    from io import BytesIO
    from PIL import Image

    app = FastAPI()
    model_id = "black-forest-labs/FLUX.1-dev"
    pipe = FluxPipeline.from_pretrained(
        model_id,
        torch_dtype=torch.float16,
        device_map="mps"
    )
    pipe.to("mps")

    @app.post("/generate")
    async def generate_image(prompt: str):
        try:
            image = pipe(prompt, num_inference_steps=20).images[0]
            buffered = BytesIO()
            image.save(buffered, format="PNG")
            img_str = base64.b64encode(buffered.getvalue()).decode("utf-8")
            return {"status": "success", "image": img_str}
        except Exception as e:
            return JSONResponse(status_code=500, content={"status": "error", "message": str(e)})

    if __name__ == "__main__":
        import uvicorn
        uvicorn.run(app, host="0.0.0.0", port=8001)
    ```
- **Run**:
  ```bash
  python flux_api.py
  ```
  - Port: 8001
- **Dify Integration**:
  - Add custom provider:
    - Model Type: Custom (Text-to-Image)
    - Model Name: `flux.1-dev`
    - Base URL: `http://localhost:8001/generate`

### whisper-base (Speech-to-Text)

- **Purpose**: Transcribes audio to text.
- **Size**: ~145 MB
- **Install whisper.cpp**:
  ```bash
  git clone https://github.com/ggerganov/whisper.cpp.git
  cd whisper.cpp
  brew install cmake
  make
  ./models/download-ggml-model.sh base
  ```
- **Setup Script**:
  - Create `whisper_api.py`:
    ```python
    # artifact_id: 8c9f2e4d-5a3b-4d8c-9e7f-7b3c4e5f6a7c
    # title: whisper_api.py
    # contentType: text/python
    from fastapi import FastAPI, UploadFile
    from fastapi.responses import JSONResponse
    import subprocess
    import os
    import tempfile

    app = FastAPI()

    @app.post("/transcribe")
    async def transcribe_audio(file: UploadFile):
        try:
            with tempfile.NamedTemporaryFile(delete=False, suffix=".wav") as temp_file:
                temp_file.write(await file.read())
                temp_path = temp_file.name
            result = subprocess.run(
                ["./main", "-m", "models/ggml-base.bin", "-f", temp_path, "-t", "8"],
                cwd=os.path.expanduser("~/whisper.cpp"),
                capture_output=True,
                text=True
            )
            os.remove(temp_path)
            if result.returncode != 0:
                raise Exception(result.stderr)
            return {"status": "success", "text": result.stdout.strip()}
        except Exception as e:
            return JSONResponse(status_code=500, content={"status": "error", "message": str(e)})

    if __name__ == "__main__":
        import uvicorn
        uvicorn.run(app, host="0.0.0.0", port=8002)
    ```
- **Run**:
  ```bash
  python whisper_api.py
  ```
  - Port: 8002
- **Dify Integration**:
  - Add custom provider:
    - Model Type: Custom (Speech-to-Text)
    - Model Name: `whisper-base`
    - Base URL: `http://localhost:8002/transcribe`

### piper-tts (Text-to-Speech)

- **Purpose**: Converts text to speech.
- **Size**: ~100 MB
- **Install**:
  ```bash
  git clone https://github.com/rhasspy/piper.git
  cd piper
  pip install -r requirements.txt
  wget https://huggingface.co/rhasspy/piper-voices/resolve/main/en_US/en_US-lessac-medium.onnx
  wget https://huggingface.co/rhasspy/piper-voices/resolve/main/en_US/en_US-lessac-medium.onnx.json
  ```
- **Setup Script**:
  - Create `piper_api.py`:
    ```python
    # artifact_id: 9d0f3f5e-6b4c-4e9d-af8g-8c4d5f6g7b8d
    # title: piper_api.py
    # contentType: text/python
    from fastapi import FastAPI
    from piper import PiperVoice
    from fastapi.responses import StreamingResponse
    import io

    app = FastAPI()
    voice = PiperVoice.load("en_US-lessac-medium.onnx")

    @app.post("/synthesize")
    async def synthesize_text(text: str):
        try:
            audio = voice.synthesize(text)
            return StreamingResponse(io.BytesIO(audio), media_type="audio/wav")
        except Exception as e:
            return {"status": "error", "message": str(e)}

    if __name__ == "__main__":
        import uvicorn
        uvicorn.run(app, host="0.0.0.0", port=8003)
    ```
- **Run**:
  ```bash
  python piper_api.py
  ```
  - Port: 8003
- **Dify Integration**:
  - Add custom provider:
    - Model Type: Custom (Text-to-Speech)
    - Model Name: `piper-tts`
    - Base URL: `http://localhost:8003/synthesize`

---

## 5. Running All Components

Start all components to ensure the multi-agent system is operational:

| Component        | Command                        | Port   |
|------------------|--------------------------------|--------|
| **Ollama**       | `ollama serve`                 | 11434  |
| **Dify**         | `cd ~/dify/docker && docker-compose up -d` | 3000 |
| **flux.1-dev**   | `python flux_api.py`           | 8001   |
| **whisper-base** | `python whisper_api.py`        | 8002   |
| **piper-tts**    | `python piper_api.py`          | 8003   |
| **Ngrok**        | `ngrok http 3000`              | Dynamic |

- **Stop Commands**:
  - APIs: `Ctrl+C` in terminal.
  - Dify: `cd ~/dify/docker && docker-compose down`

---

## 6. Organizing Documentation

To ensure accessibility and maintainability, organize this documentation in Dify’s Knowledge Base or a Git repository:

1. **Dify Knowledge Base**:
   - **Create**: In Dify, go to **Knowledge** > **Create Knowledge Base**.
   - **Name**: `Dify Setup Documentation`
   - **Embedding Model**: `nomic-embed-text:latest`
   - **Upload**: Save this content as `dify_setup.md` and upload:
     ```bash
     echo "# Dify Installation and Setup Documentation..." > ~/dify_setup.md
     ```
   - **Tags**: `Installation`, `Ollama`, `Ngrok`, `Custom Components`, `Multi-Agent`

2. **Sub-Documents**:
   - Split into:
     - `dify_installation.md`: Dify setup steps.
     - `ngrok_setup.md`: Ngrok installation and configuration.
     - `ollama_models.md`: Ollama model details.
     - `custom_components.md`: flux.1-dev, whisper-base, piper-tts.

3. **Search Workflow**:
   - Create a Dify workflow to query the Knowledge Base:
     - **Input Node**: Query (e.g., “How to install Ngrok?”).
     - **Search Node**: Use `bge-small-en-v1.5` for retrieval.
     - **Summarizer Node**: Use `phi3:3.8b` to summarize.
     - **Output Node**: Return results.

4. **Git Repository**:
   - Host on GitHub for version control:
     ```bash
     mkdir ~/dify-setup-docs
     cd ~/dify-setup-docs
     git init
     cp ~/dify_setup.md .
     git add dify_setup.md
     git commit -m "Initial Dify setup documentation"
     git remote add origin https://github.com/yourusername/dify-setup-docs.git
     git push -u origin main
     ```
   - **Versioning**: Tag releases:
     ```bash
     git tag v1.0
     git push origin v1.0
     ```

5. **Access Control**:
   - In Dify, restrict Knowledge Base access to your team via **Settings** > **Permissions**.

---

## 7. Testing and Validation

Ensure all components work as expected:

- **Dify**:
  - Test: `curl http://localhost:3000/apps`
  - Verify: Dify dashboard loads at `http://192.168.50.122:3000`.

- **Ngrok**:
  - Test: Access `https://abc123.ngrok.io/apps` on phone (mobile data).
  - Verify: App list loads.

- **Ollama Models**:
  - Test: `ollama run llava:latest "Hello"`
  - Verify: Model responds (e.g., image description for `llava`).

- **Custom Components**:
  - Test APIs:
    ```bash
    curl http://localhost:8001/generate -d '{"prompt": "A futuristic city"}'
    curl -X POST http://localhost:8002/transcribe -F "file=@~/whisper.cpp/samples/jfk.wav"
    curl -X POST http://localhost:8003/synthesize -d '{"text": "Test narration"}'
    ```

- **Organization**:
  - Upload to Knowledge Base and query: “How to install Ollama models?”
  - Verify: Relevant sections retrieved.

---

## 8. Troubleshooting

| Issue                       | Solution                                                                 |
|-----------------------------|--------------------------------------------------------------------------|
| **Dify Connection Refused** | Check Docker: `docker ps` <br> Free port 3000: `lsof -i :3000 && sudo kill -9 <PID>` <br> Logs: `docker logs dify-nginx-1` |
| **Ngrok Command Not Found** | Ensure PATH: `echo 'export PATH="/usr/local/bin:$PATH"' >> ~/.zshrc` <br> Reinstall: `brew install ngrok/ngrok/ngrok` |
| **Ollama Not Responding**   | Run: `ollama serve` <br> Test: `curl http://localhost:11434`             |
| **Custom API Errors**       | Test: `curl http://localhost:8003/synthesize -d '{"text": "Test"}'` <br> Check logs or restart API |
| **PluginDaemonBadRequestError** | Clear: `rm -rf ~/dify/docker/plugins/yourusername_plugin-name` <br> Waive: `echo "FORCE_VERIFYING_SIGNATURE=false" >> ~/dify/docker/.env` <br> Restart: `docker-compose restart` |
| **External Access Fails**   | Test local: `curl http://192.168.50.122:3000` <br> Firewall: `sudo /usr/libexec/ApplicationFirewall/socketfilterfw --add /usr/local/bin/docker` |

---

## Why This Layout?
- **Consistent Headings**: Clear hierarchy with `#`, `##`, `###` for easy navigation.
- **Tables**: Summarize model details and troubleshooting for quick reference.
- **Code Blocks**: Highlight commands and scripts for clarity.
- **Bullet Points**: Break down prerequisites and steps for readability.
- **Table of Contents**: Enables quick access to sections.
- **Organized Sections**: Separates Dify, Ngrok, Ollama, and custom components for clarity.

This enhanced Markdown is ready for Dify’s Knowledge Base or GitHub, ensuring accessibility and maintainability for your multi-agent system setup.
