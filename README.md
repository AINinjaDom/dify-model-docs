# Model Documentation for Multi-Agent System on Mac Mini M4 Pro

This document details the specifications, strengths, and use cases for AI models integrated with Ollama and Dify on a Mac Mini M4 Pro (14-core CPU, up to 20-core GPU, 16GB+ RAM, macOS Sequoia, as of July 27, 2025, 01:13 AM HKT). The models power a modern, capable, and fun multi-agent system for reasoning, vision, image generation, coding, search, speech-to-text, text-to-speech, and conversational tasks (including potential Cantonese support). It includes setup for external access via Ngrok and is designed for Dify’s Knowledge Base.

## Hardware and Software Context
- **Mac Mini M4 Pro**: 14-core CPU, 20-core GPU, 16-core Neural Engine (38 TOPS), 16GB+ RAM, ~500GB+ storage.
- **Ollama**: Runs at `http://host.docker.internal:11434`. Models: `llava:latest`, `gemma2:latest`, `nomic-embed-text:latest`, `llama3.2:latest`, `qwen2.5:14b`, `mistral:7b`, `phi3:3.8b`, `bge-small-en-v1.5`, `bakllava`, `codellama:7b`, `borch/llama3_speed_chat`, `wangshenzhi/llama3-8b-chinese-chat`.
- **Dify**: Docker-based, accessible locally at `http://192.168.50.122:3000`. Supports multi-agent workflows.
- **External Access**: Configured for phone access via Ngrok (`https://<ngrok-url>/apps`), Wi-Fi (`http://192.168.50.122:3000/apps`), or VPN.

## Models and Specifications

### 1. llava:latest
- **Type**: LLM with Vision
- **Size**: ~4.7 GB
- **Recommended Specs**: 8GB RAM, M4 Pro GPU, 5GB storage, 4096-token context, 4096 max tokens.
- **Strengths**: Multimodal text and image processing, excels in image description and visual Q&A.
- **Use Cases**: Visual Analyst Agent (e.g., “Describe this photo”).
- **Dify Settings**:
  - Model Type: LLM
  - Model Name: `llava:latest`
  - Base URL: `http://host.docker.internal:11434`
  - Completion Mode: Chat
  - Model Context Size: 4096
  - Upper Bound for Max Tokens: 4096
  - Vision Support: Yes
  - Function Call Support: No

### 2. gemma2:latest
- **Type**: LLM
- **Size**: ~5.4 GB
- **Recommended Specs**: 8GB RAM, M4 Pro GPU, 6GB storage, 8192-token context, 4096 max tokens.
- **Strengths**: High-quality text generation for conversations and reasoning.
- **Use Cases**: Narrative Agent (e.g., “Write a sci-fi story”).
- **Dify Settings**:
  - Model Type: LLM
  - Model Name: `gemma2:latest`
  - Base URL: `http://host.docker.internal:11434`
  - Completion Mode: Chat
  - Model Context Size: 8192
  - Upper Bound for Max Tokens: 4096
  - Vision Support: No
  - Function Call Support: No

### 3. nomic-embed-text:latest
- **Type**: Text Embedding
- **Size**: ~274 MB
- **Recommended Specs**: 4GB RAM, CPU, 300MB storage, 8192-token context.
- **Strengths**: Lightweight, high-quality embeddings for search and RAG.
- **Use Cases**: Search Agent (e.g., “Find AI papers”).
- **Dify Settings**:
  - Model Type: Text Embedding
  - Model Name: `nomic-embed-text:latest`
  - Base URL: `http://host.docker.internal:11434`
  - Completion Mode: Not applicable
  - Model Context Size: 8192
  - Upper Bound for Max Tokens: Not applicable
  - Vision Support: No
  - Function Call Support: No

### 4. llama3.2:latest
- **Type**: LLM
- **Size**: ~2.0 GB
- **Recommended Specs**: 4GB RAM, M4 Pro GPU, 2.5GB storage, 4096-token context, 4096 max tokens.
- **Strengths**: Lightweight, fast, supports function calling.
- **Use Cases**: Tool Agent (e.g., “Fetch weather data”).
- **Dify Settings**:
  - Model Type: LLM
  - Model Name: `llama3.2:latest`
  - Base URL: `http://host.docker.internal:11434`
  - Completion Mode: Chat
  - Model Context Size: 4096
  - Upper Bound for Max Tokens: 4096
  - Vision Support: No
  - Function Call Support: Yes

### 5. qwen2.5:14b
- **Type**: LLM
- **Size**: ~9.0 GB
- **Recommended Specs**: 16GB RAM, M4 Pro GPU, 10GB storage, 32768-token context, 4096 max tokens.
- **Strengths**: Advanced reasoning, large context, function calling.
- **Use Cases**: Reasoner Agent (e.g., “Plan a complex project”).
- **Dify Settings**:
  - Model Type: LLM
  - Model Name: `qwen2.5:14b`
  - Base URL: `http://host.docker.internal:11434`
  - Completion Mode: Chat
  - Model Context Size: 32768
  - Upper Bound for Max Tokens: 4096
  - Vision Support: No
  - Function Call Support: Yes

### 6. mistral:7b
- **Type**: LLM
- **Size**: ~4.1 GB
- **Recommended Specs**: 8GB RAM, M4 Pro GPU, 5GB storage, 8192-token context, 4096 max tokens.
- **Strengths**: Efficient reasoning and chat, fast.
- **Use Cases**: Planner Agent (e.g., “Decompose a game project”).
- **Dify Settings**:
  - Model Type: LLM
  - Model Name: `mistral:7b`
  - Base URL: `http://host.docker.internal:11434`
  - Completion Mode: Chat
  - Model Context Size: 8192
  - Upper Bound for Max Tokens: 4096
  - Vision Support: No
  - Function Call Support: Yes

### 7. phi3:3.8b
- **Type**: LLM
- **Size**: ~2.3 GB
- **Recommended Specs**: 4GB RAM, CPU, 2.5GB storage, 4096-token context, 2048 max tokens.
- **Strengths**: Ultra-lightweight, fast for simple tasks.
- **Use Cases**: Junior Assistant Agent (e.g., “Summarize text”).
- **Dify Settings**:
  - Model Type: LLM
  - Model Name: `phi3:3.8b`
  - Base URL: `http://host.docker.internal:11434`
  - Completion Mode: Chat
  - Model Context Size: 4096
  - Upper Bound for Max Tokens: 2048
  - Vision Support: No
  - Function Call Support: Yes

### 8. bge-small-en-v1.5
- **Type**: Text Embedding
- **Size**: ~133 MB
- **Recommended Specs**: 2GB RAM, CPU, 200MB storage, 512-token context.
- **Strengths**: Compact, high-quality English embeddings.
- **Use Cases**: Search Agent (e.g., “Retrieve relevant data”).
- **Dify Settings**:
  - Model Type: Text Embedding
  - Model Name: `bge-small-en-v1.5`
  - Base URL: `http://host.docker.internal:11434`
  - Completion Mode: Not applicable
  - Model Context Size: 512
  - Upper Bound for Max Tokens: Not applicable
  - Vision Support: No
  - Function Call Support: No

### 9. bakllava
- **Type**: LLM with Vision
- **Size**: ~4.5 GB
- **Recommended Specs**: 8GB RAM, M4 Pro GPU, 5GB storage, 4096-token context, 4096 max tokens.
- **Strengths**: Efficient vision and text processing.
- **Use Cases**: Visual Analyst Agent (e.g., “Analyze story images”).
- **Dify Settings**:
  - Model Type: LLM
  - Model Name: `bakllava`
  - Base URL: `http://host.docker.internal:11434`
  - Completion Mode: Chat
  - Model Context Size: 4096
  - Upper Bound for Max Tokens: 4096
  - Vision Support: Yes
  - Function Call Support: No

### 10. codellama:7b
- **Type**: LLM for Code Generation
- **Size**: ~3.8 GB
- **Recommended Specs**: 8GB RAM, M4 Pro GPU, 4GB storage, 4096-token context, 2048 max tokens.
- **Strengths**: Specialized for coding tasks.
- **Use Cases**: Developer Agent (e.g., “Code a Python game”).
- **Dify Settings**:
  - Model Type: LLM
  - Model Name: `codellama:7b`
  - Base URL: `http://host.docker.internal:11434`
  - Completion Mode: Chat
  - Model Context Size: 4096
  - Upper Bound for Max Tokens: 2048
  - Vision Support: No
  - Function Call Support: Yes

### 11. flux.1-dev
- **Type**: Text-to-Image
- **Size**: ~12 GB
- **Recommended Specs**: 16GB RAM (32GB preferred), M4 Pro GPU (Metal via `diffusers`), 15GB storage.
- **Strengths**: High-quality image generation.
- **Use Cases**: Creative Agent (e.g., “Illustrate a futuristic city”).
- **Setup**:
  - Install `pip` if missing:
    ```bash
    curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
    python3 get-pip.py
    ```
  - Install PyTorch nightly (CPU-only, as used):
    ```bash
    pip3 install --pre torch torchvision torchaudio --index-url https://download.pytorch.org/whl/nightly/cpu
    ```
    - Note: For M4 Pro GPU (MPS) support, use:
      ```bash
      pip3 install --pre torch torchvision torchaudio --index-url https://download.pytorch.org/whl/nightly
      ```
      or stable:
      ```bash
      pip3 install torch torchvision torchaudio
      ```
  - Install `DeepSpeed`:
    ```bash
    pip install DeepSpeed
    ```
  - Install other dependencies:
    ```bash
    pip install --upgrade diffusers transformers torch torchvision torchaudio accelerate fastapi uvicorn protobuf sentencepiece
    ```
  - Build `sentencepiece` if needed:
    ```bash
    git clone https://github.com/google/sentencepiece.git
    cd sentencepiece
    mkdir build
    cd build
    cmake .. -DCMAKE_POLICY_VERSION_MINIMUM=3.5
    make -j$(gnproc)
    sudo make install
    cd ../python
    pip install .
    ```
  - Configure `accelerate`:
    ```bash
    accelerate config
    ```
    - Select MPS, fp16, 1 GPU.
  - Update `flux_api.py` with Hugging Face token and run:
    ```bash
    python3 flux_api.py
    ```
    - Port: 8001
  - Test:
    ```bash
    curl -X POST http://localhost:8001/generate -H "Content-Type: application/json" -d '{"prompt": "A futuristic city at sunset"}'
    ```
  - Authenticate: Set `HUGGINGFACE_TOKEN` or add token in script.
- **Dify Settings**:
  - Model Type: Custom (Text-to-Image)
  - Model Name: `flux.1-dev`
  - Base URL: `http://localhost:8001/generate`
  - Completion Mode: Not applicable
  - Model Context Size: Not applicable
  - Upper Bound for Max Tokens: Not applicable
  - Vision Support: No
  - Function Call Support: No

### 12. whisper-base
- **Type**: Speech-to-Text
- **Size**: ~145 MB
- **Recommended Specs**: 4GB RAM, CPU, 200MB storage.
- **Strengths**: Accurate speech transcription, optimized for Apple Silicon.
- **Use Cases**: Voice Input Agent (e.g., “Transcribe user commands”).
- **Setup**:
  - Install:
    ```bash
    git clone https://github.com/ggerganov/whisper.cpp.git
    cd whisper.cpp
    make
    ./models/download-ggml-model.sh base
    ```
  - Run API:
    ```bash
    python whisper_api.py
    ```
    - Port: 8002
- **Dify Settings**:
  - Model Type: Custom (Speech-to-Text)
  - Model Name: `whisper-base`
  - Base URL: `http://localhost:8002/transcribe`
  - Completion Mode: Not applicable
  - Model Context Size: Not applicable
  - Upper Bound for Max Tokens: Not applicable
  - Vision Support: No
  - Function Call Support: No

### 13. piper-tts
- **Type**: Text-to-Speech
- **Size**: ~100 MB
- **Recommended Specs**: 2GB RAM, CPU, 150MB storage.
- **Strengths**: Natural-sounding speech, lightweight.
- **Use Cases**: Voice Output Agent (e.g., “Narrate a story”).
- **Setup**:
  - Install:
    ```bash
    git clone https://github.com/rhasspy/piper.git
    cd piper
    pip install -r requirements.txt
    wget https://huggingface.co/rhasspy/piper-voices/resolve/main/en_US/en_US-lessac-medium.onnx
    wget https://huggingface.co/rhasspy/piper-voices/resolve/main/en_US/en_US-lessac-medium.onnx.json
    ```
  - Run API:
    ```bash
    python piper_api.py
    ```
    - Port: 8003
- **Dify Settings**:
  - Model Type: Custom (Text-to-Speech)
  - Model Name: `piper-tts`
  - Base URL: `http://localhost:8003/synthesize`
  - Completion Mode: Not applicable
  - Model Context Size: Not applicable
  - Upper Bound for Max Tokens: Not applicable
  - Vision Support: No
  - Function Call Support: No

### 14. borch/llama3_speed_chat
- **Type**: LLM
- **Size**: ~4.5 GB
- **Recommended Specs**: 8GB RAM, M4 Pro GPU, 5GB storage, 4096-token context, 2048 max tokens.
- **Strengths**: Fast, conversational responses, optimized for speech-to-text input, supports function calling.
- **Use Cases**: Conversational Agent (e.g., “Quick chat responses”), pairs with `whisper-base` and `piper-tts`.
- **Cantonese Support**: Limited; test with Cantonese prompts (e.g., “用廣東話講個笑話”).
- **Setup**:
  - Install:
    ```bash
    ollama pull borch/llama3_speed_chat
    ```
- **Dify Settings**:
  - Model Type: LLM
  - Model Name: `borch/llama3_speed_chat`
  - Base URL: `http://host.docker.internal:11434`
  - Completion Mode: Chat
  - Model Context Size: 4096
  - Upper Bound for Max Tokens: 2048
  - Vision Support: No
  - Function Call Support: Yes

### 15. wangshenzhi/llama3-8b-chinese-chat
- **Type**: LLM
- **Size**: ~4.5 GB
- **Recommended Specs**: 8GB RAM, M4 Pro GPU, 5GB storage, 8192-token context, 4096 max tokens.
- **Strengths**: Fine-tuned for Chinese (Mandarin, likely better for Cantonese), supports roleplay and tools.
- **Use Cases**: Conversational Agent for Chinese/Cantonese (e.g., “Write about Hong Kong culture”).
- **Setup**:
  - Install:
    ```bash
    ollama pull wangshenzhi/llama3-8b-chinese-chat
    ```
- **Dify Settings**:
  - Model Type: LLM
  - Model Name: `wangshenzhi/llama3-8b-chinese-chat`
  - Base URL: `http://host.docker.internal:11434`
  - Completion Mode: Chat
  - Model Context Size: 8192
  - Upper Bound for Max Tokens: 4096
  - Vision Support: No
  - Function Call Support: Yes

## Multi-Agent System Example
- **Workflow**: Cantonese storytelling app.
  - **Voice Input** (`whisper-base`): Transcribes Cantonese voice (e.g., “講一個香港故事”).
  - **Conversational Agent** (`wangshenzhi/llama3-8b-chinese-chat` or `borch/llama3_speed_chat`): Generates story in Cantonese.
  - **Narrator** (`gemma2:latest`): Adds English translation if needed.
  - **Visual Analyst** (`llava:latest`, `bakllava`): Describes story-related images.
  - **Image Creator** (`flux.1-dev`): Generates visuals.
  - **Coder** (`codellama:7b`): Codes an interactive story app.
  - **Searcher** (`nomic-embed-text:latest`, `bge-small-en-v1.5`): Retrieves cultural references.
  - **Planner** (`mistral:7b`): Coordinates tasks.
  - **Reasoner** (`qwen2.5:14b`): Refines story logic.
  - **Assistant** (`phi3:3.8b`, `llama3.2:latest`): Handles queries.
  - **Voice Output** (`piper-tts`): Narrates story in English or Mandarin (Cantonese TTS may require external API).

## Integration Notes
- **Ollama**:
  - Install: `ollama pull borch/llama3_speed_chat`, `ollama pull wangshenzhi/llama3-8b-chinese-chat`
  - Verify: `ollama list`
  - Run: `ollama serve`
- **Custom APIs**:
  - `flux.1-dev`: Run `flux_api.py` (port 8001).
  - `whisper-base`: Run `whisper_api.py` (port 8002).
  - `piper-tts`: Run `piper_api.py` (port 8003).
- **Dify**:
  - Update `config.yaml` as above.
  - Restart:
    ```bash
    cd ~/dify/docker
    docker-compose down
    docker-compose up -d
    ```
- **Plugin Error Handling**:
  - Clear duplicates:
    ```bash
    rm -rf ~/dify/docker/plugins/yourusername_plugin-name
    docker exec dify-db-1 psql -U postgres -d dify -c "DELETE FROM plugins;"
    ```
  - Waive verification:
    ```bash
    echo "FORCE_VERIFYING_SIGNATURE=false" >> ~/dify/docker/.env
    ```
  - Restart Dify.

## External Access Setup
- **Ngrok** (Primary Method):
  - **Setup**:
    - Verify authtoken: `cat "/Users/dominicyu/Library/Application Support/ngrok/ngrok.yml"`
    - Run: `ngrok http 3000`
    - Access: `https://<ngrok-url>/apps` (e.g., `https://abc123.ngrok.io/apps`)
  - **Security**: Use HTTPS, enable Dify authentication (**Settings** > **Security**).
  - **Limitations**: Free URLs are temporary; paid plans offer static domains.
- **Same Wi-Fi**:
  - Access: `http://192.168.50.122:3000/apps`
  - Firewall:
    ```bash
    sudo /usr/libexec/ApplicationFirewall/socketfilterfw --add /usr/local/bin/docker
    ```
- **External (Mobile Data)**:
  - **VPN** (Recommended):
    - Install Tailscale:
      ```bash
      brew install tailscale
      tailscale up
      ```
    - Connect phone to Tailscale network.
    - Access: `http://192.168.50.122:3000/apps`
  - **Port Forwarding**:
    - Router: Forward port 3000 to `192.168.50.122:3000` (TCP).
    - Public IP: `curl ifconfig.me` (e.g., `203.0.113.1`).
    - Access: `http://203.0.113.1:3000/apps`
    - DDNS: Use DuckDNS (`yourdify.duckdns.org`) for dynamic IP.
  - **Reverse Proxy with HTTPS**:
    - Install Caddy:
      ```bash
      brew install caddy
      ```
    - Create Caddyfile:
      ```bash
      echo "yourdify.duckdns.org { reverse_proxy http://192.168.50.122:3000; tls your.email@example.com }" > ~/Caddyfile
      caddy run --config ~/Caddyfile
      ```
    - Forward router port 443 to Mac’s port 80.
    - Access: `https://yourdify.duckdns.org/apps`

## Organizing Documentation in Dify
- **Knowledge Base**:
  - Create: **Knowledge** > **Create Knowledge Base** > Name: `Model Documentation`.
  - Upload: Save this content as `model_documentation.md` and upload.
  - Embedding Model: `nomic-embed-text:latest`.
  - Tags: `LLM`, `Vision`, `Embedding`, `Text-to-Image`, `Code`, `Speech-to-Text`, `Text-to-Speech`, `Cantonese`, `Ngrok`.
- **Workflow**: Create a query workflow:
  - Input: Query (e.g., “How to set up FLUX.1-dev?”).
  - Search: `bge-small-en-v1.5` retrieves sections.
  - Summarizer: `phi3:3.8b` summarizes results.
  - Output: Returns response.
- **Version Control**: Host in Git (e.g., `https://github.com/yourusername/dify-docs`).
- **Access Control**: Restrict to team members in Dify’s permissions settings.

## Testing Recommendations
- **MPS Usage** (if using MPS-enabled PyTorch)**:
  - Verify:
    ```bash
    python3 -c "import torch; print('MPS available:', torch.backends.mps.is_available()); print('PyTorch version:', torch.__version__)"
    ```
  - Monitor GPU usage in Activity Monitor during generation.
- **Flux.1 API**:
  - Run:
    ```bash
    python3 ~/flux_api.py
    ```
  - Test:
    ```bash
    curl -X POST http://localhost:8001/generate -H "Content-Type: application/json" -d '{"prompt": "A futuristic city at sunset"}'
    ```
  - Verify: Image generated (faster with MPS; slower with CPU-only PyTorch).
- **Dify Workflow**:
  - Test: Workflow with `flux.1-dev` node (prompt: “A serene mountain landscape”).
  - Verify: Image generated.
- **External Access**:
  - Run:
    ```bash
    ngrok http 3000
    ```
  - Access: `https://<ngrok-url>/apps` on phone.
  - Test workflow remotely.
- **Cantonese Testing**:
  - Test:
    ```bash
    ollama run wangshenzhi/llama3-8b-chinese-chat "用廣東話講一個笑話"
    ```
  - Compare with `borch/llama3_speed_chat`.
- **Performance**:
  - Monitor RAM/GPU in Activity Monitor (~40GB total model size).
  - Use lighter models (e.g., `phi3:3.8b`) if 16GB RAM is strained.

## Troubleshooting
- **MPS Not Available** (if using MPS-enabled PyTorch):
  - Check PyTorch version:
    ```bash
    python3 -c "import torch; print(torch.__version__)"
    ```
  - Reinstall:
    ```bash
    pip3 install torch torchvision torchaudio
    ```
  - Ensure macOS Sequoia and M4 Pro compatibility.
- **Slow Generation**:
  - Check logs:
    ```bash
    tail -f flux_api.log
    ```
  - Verify MPS (if enabled):
    ```bash
    python3 -c "import torch; print(torch.backends.mps.is_available())"
    ```
  - Adjust `num_inference_steps` (e.g., 10) or resolution (`height=256`, `width=256`) in `flux_api.py`.
- **Sentencepiece**:
  - Verify:
    ```bash
    python3 -c "import sentencepiece; print(sentencepiece.__version__)"
    ```
  - Rebuild:
    ```bash
    git clone https://github.com/google/sentencepiece.git
    cd sentencepiece
    mkdir build
    cd build
    cmake .. -DCMAKE_POLICY_VERSION_MINIMUM=3.5
    make -j$(gnproc)
    sudo make install
    cd ../python
    pip install .
    ```
- **DeepSpeed**:
  - Verify:
    ```bash
    python3 -c "import deepspeed; print(deepspeed.__version__)"
    ```
  - Reinstall:
    ```bash
    pip install DeepSpeed
    ```
- **Dify Integration**:
  - Check logs:
    ```bash
    docker logs dify-api-1
    ```
- **Plugin Errors**:
  - Check logs:
    ```bash
    docker logs dify-plugin-daemon-1
    ```
  - Clear:
    ```bash
    rm -rf ~/dify/docker/plugins/yourusername_plugin-name
    docker exec dify-db-1 psql -U postgres -d dify -c "DELETE FROM plugins;"
    ```
- **Ngrok Access**:
  - Verify:
    ```bash
    ngrok config check
    ```
  - Test:
    ```bash
    curl http://localhost:3000/apps
    ```
