# Model Documentation for Multi-Agent System on Mac Mini M4 Pro

This document outlines the recommended specifications, strengths, and use cases for the selected AI models integrated with Ollama and Dify on a Mac Mini M4 Pro (14-core CPU, up to 20-core GPU, 16GB+ RAM, macOS Sequoia). These models support a modern, capable, and fun multi-agent system for tasks like reasoning, vision, image generation, coding, and search. The document is organized for easy reference within Dify.

## Hardware Context
- **Mac Mini M4 Pro**: 14-core CPU, up to 20-core GPU, 16-core Neural Engine (38 TOPS), 16GB+ RAM, ~500GB+ storage.
- **Ollama**: Runs at `http://host.docker.internal:11434` for Dify integration.
- **Dify**: Docker-based, supports multi-agent workflows via plugins and model providers.

## Models and Specifications

### 1. llava:latest
- **Type**: Large Language Model (LLM) with Vision
- **Size**: ~4.7 GB
- **Recommended Specs**:
  - RAM: 8GB (16GB preferred for multitasking)
  - GPU: M4 Pro’s 20-core GPU (Metal acceleration via Ollama)
  - Storage: 5GB free
  - Context Size: 4096 tokens
  - Max Tokens: 4096 (reduce to 2048 if memory-limited)
- **Strengths**:
  - Multimodal: Processes text and images.
  - Excels in image description, visual question answering (VQA), and scene analysis.
- **Use Cases in Multi-Agent System**:
  - **Visual Analyst Agent**: Describes images (e.g., “What’s in this photo?”) or answers visual queries (e.g., “What text is in this screenshot?”).
  - Collaborates with text agents (e.g., `gemma2`) for storytelling or analysis.
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
- **Type**: Large Language Model (LLM)
- **Size**: ~5.4 GB
- **Recommended Specs**:
  - RAM: 8GB (16GB preferred)
  - GPU: M4 Pro GPU (Metal acceleration)
  - Storage: 6GB free
  - Context Size: 8192 tokens
  - Max Tokens: 4096 (up to 8192 with 32GB RAM)
- **Strengths**:
  - High-quality text generation for conversational and reasoning tasks.
  - Efficient for chat-based interactions.
- **Use Cases in Multi-Agent System**:
  - **Narrative Agent**: Generates stories, dialogues, or explanations (e.g., “Write a sci-fi story”).
  - Supports reasoning tasks for other agents (e.g., summarizes outputs from `llava`).
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
- **Recommended Specs**:
  - RAM: 4GB (minimal footprint)
  - GPU: Optional (CPU sufficient)
  - Storage: 300MB free
  - Context Size: 8192 tokens
- **Strengths**:
  - Generates high-quality text embeddings for semantic search and similarity tasks.
  - Lightweight and fast.
- **Use Cases in Multi-Agent System**:
  - **Search Agent**: Retrieves relevant documents or data (e.g., “Find AI research papers”).
  - Enhances RAG (Retrieval-Augmented Generation) for other agents (e.g., feeds context to `qwen2.5`).
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
- **Type**: Large Language Model (LLM)
- **Size**: ~2.0 GB
- **Recommended Specs**:
  - RAM: 4GB (8GB preferred)
  - GPU: M4 Pro GPU (Metal acceleration)
  - Storage: 2.5GB free
  - Context Size: 4096 tokens
  - Max Tokens: 4096 (reduce to 2048 for speed)
- **Strengths**:
  - Lightweight and fast for chat and reasoning.
  - Supports function calling for tool integration.
- **Use Cases in Multi-Agent System**:
  - **Tool Agent**: Executes API calls or tools (e.g., “Fetch weather data”).
  - Quick-response agent for simple queries or task coordination.
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
- **Type**: Large Language Model (LLM)
- **Size**: ~9.0 GB
- **Recommended Specs**:
  - RAM: 16GB (32GB preferred for large context)
  - GPU: M4 Pro GPU (Metal acceleration)
  - Storage: 10GB free
  - Context Size: 32768 tokens
  - Max Tokens: 4096 (up to 8192 with 32GB RAM)
- **Strengths**:
  - Advanced reasoning with large context window.
  - Supports function calling for complex tasks.
- **Use Cases in Multi-Agent System**:
  - **Reasoner Agent**: Handles complex tasks (e.g., “Write a 500-word essay on AI ethics”).
  - Coordinates multi-step workflows by processing outputs from other agents.
- **Dify Settings**:
  - Model Type: LLM
  - Model Name: `qwen2.5:14b`
  - Base URL: `http://host.docker.internal:8888`
  - Completion Mode: Chat
  - Model Context Size: 32768
  - Upper Bound for Max Tokens: 2048
  - Vision Support: Yes
  - Function Call Support: Yes

### 6. mistral:7b
- **Type**: Large Language Model (LLM)
- **Size**: ~4.1 GB
- **Recommended Specs**:
  - RAM: 8GB
  - GPU: M4 Pro GPU
  - Storage: 5GB free
  - Context Size: 8192 tokens
  - Max Tokens: 4096
- **Strengths**:
  - Efficient and versatile reasoning and chat.
  - Fast for task planning and coordination.
- **Use Cases**:
  - **Planner Agent**: Decomposes tasks (e.g., “Plan a game project”).
  - Witty conversational agent for user interaction.
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
- **Type**: Large Language Model (LLM)
- **Size**: ~2.3 GB
- **Recommended Specs**:
  - RAM: 4GB
  - GPU: Optional (CPU sufficient)
  - Storage: 2.5GB free
  - Context Size: 4096 tokens
  - Max Tokens: 2048
- **Strengths**:
  - Ultra-lightweight, fast responses.
  - Ideal for simple tasks or support roles.
- **Use Cases**:
  - **Junior Assistant Agent**: Handles FAQs or summarizes outputs.
  - Quick-response agent for lightweight tasks.
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
- **Recommended Specs**:
  - RAM: 2GB
  - GPU: Optional
  - Storage: 200MB free
  - Context Size: 512 tokens
- **Strengths**:
  - Compact, high-quality embeddings for English text.
  - Fast for search and retrieval.
- **Use Cases**:
  - **Search Agent**: Retrieves relevant data for other agents.
  - Enhances RAG workflows.
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
- **Type**: Large Language Model (LLM) with Vision
- **Size**: ~4.5 GB
- **Recommended Specs**:
  - RAM: 8GB
  - GPU: M4 Pro GPU
  - Storage: 5GB free
  - Context Size: 4096 tokens
  - Max Tokens: 4096
- **Strengths**:
  - Efficient vision and text processing.
  - Good for creative visual tasks.
- **Use Cases**:
  - **Visual Analyst Agent**: Describes or analyzes images for storytelling.
  - Complements `llava` for diverse vision tasks.
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
- **Type**: Large Language Model (LLM) for Code Generation
- **Size**: ~3.8 GB
- **Recommended Specs**:
  - RAM: 8GB
  - GPU: M4 Pro GPU
  - Storage: 4GB free
  - Context Size: 4096 tokens
  - Max Tokens: 2048
- **Strengths**:
  - Specialized for coding tasks.
  - Generates accurate code snippets.
- **Use Cases**:
  - **Developer Agent**: Writes or debugs code (e.g., “Code a Python game”).
  - Collaborates with planner agents for app development.
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
- **Recommended Specs**:
  - RAM: 16GB (32GB preferred)
  - GPU: M4 Pro GPU (Metal via `diffusers`)
  - Storage: 15GB free
  - Context Size: Not applicable
  - Max Tokens: Not applicable
- **Strengths**:
  - Generates high-quality images from text prompts.
  - Fun for creative workflows.
- **Use Cases**:
  - **Creative Agent**: Illustrates stories or concepts (e.g., “A futuristic city”).
  - Enhances visual output for multi-agent systems.
- **Dify Settings**:
  - Model Type: Custom (Text-to-Image)
  - Model Name: `flux.1-dev`
  - Base URL: `http://localhost:8001/generate`
  - Completion Mode: Not applicable
  - Model Context Size: Not applicable
  - Upper Bound for Max Tokens: Not applicable
  - Vision Support: No
  - Function Call Support: No

## Multi-Agent System Roles
These models enable a collaborative multi-agent system:
- **Planner** (`mistral:7b`): Decomposes tasks (e.g., “Plan a game project”).
- **Narrator** (`gemma2:latest`, `qwen2.5:14b`): Generates stories or explanations.
- **Visual Analyst** (`llava:latest`, `bakllava`): Processes images for descriptions or Q&A.
- **Image Creator** (`flux.1-dev`): Generates visuals for stories or designs.
- **Coder** (`codellama:7b`): Writes code for apps or games.
- **Searcher** (`nomic-embed-text:latest`, `bge-small-en-v1.5`): Retrieves relevant data.
- **Assistant** (`phi3:3.8b`, `llama3.2:latest`): Handles quick tasks or tool calls.

## Integration Notes
- **Ollama**: Models (except `flux.1-dev`) are served at `http://host.docker.internal:11434`. Ensure Ollama runs:
  ```
  ollama serve
  ```
- **Flux.1-dev**: Run via `diffusers` with `flux_api.py` (port 8001).
- **Dify**: Configure models in **Settings** > **Model Providers**. Restart after changes:
  ```
  cd ~/dify/docker
  docker-compose down
  docker-compose up -d
  ```
- **Plugin Error**: If `PluginDaemonBadRequestError` occurs for multi-agent plugins:
  - Clear duplicates:
    ```
    rm -rf ~/dify/docker/plugins/yourusername_plugin-name
    docker exec dify-db-1 psql -U postgres -d dify -c "DELETE FROM plugins;"
    ```
  - Waive verification:
    ```
    echo "FORCE_VERIFYING_SIGNATURE=false" >> ~/dify/docker/.env
    ```
  - Restart Dify.

## Organizing Documentation in Dify

### Recommended Structure
To keep this documentation accessible within Dify, store it as a **Knowledge Base** or **Document** in Dify’s interface, leveraging its search and collaboration features. Here’s how:

1. **Create a Knowledge Base**:
   - In Dify, go to **Knowledge** > **Create Knowledge Base**.
   - Name: `Model Documentation`
   - Description: “Documentation for multi-agent system models on Mac Mini M4 Pro.”
   - Use `nomic-embed-text:latest` or `bge-small-en-v1.5` for embeddings to enable semantic search.

2. **Upload Documentation**:
   - Convert this Markdown file to a `.md` file locally:
     ```
     echo "# Model Documentation..." > ~/model_documentation.md
     ```
     Paste the content above.
   - In the Knowledge Base, click **Add Document** > **Upload File**.
   - Upload `model_documentation.md`.
   - Enable indexing with your embedding model.

3. **Organize Sections**:
   - Create sub-documents or tags for each model (e.g., `llava`, `flux.1-dev`) to allow quick retrieval.
   - Use Dify’s tagging: `LLM`, `Text Embedding`, `Text-to-Image`, `Vision`, `Code Generation`.

4. **Integrate with Workflows**:
   - Create a workflow to query the Knowledge Base:
     - **Input Node**: User query (e.g., “What is llava good for?”).
     - **Search Node**: Uses `nomic-embed-text` to retrieve relevant sections.
     - **Response Node**: Summarizes using `phi3:3.8b` or `mistral:7b`.
   - This makes the documentation interactive for your team.

5. **Version Control**:
   - Store the `.md` file in a Git repository (e.g., `https://github.com/yourusername/dify-docs`).
   - Sync updates via Dify’s Git integration or manual uploads.
   - Tag versions (e.g., `v1.0`, `v1.1`) for tracking changes.

6. **Access Control**:
   - Set permissions in Dify to restrict access to your team or specific roles.
   - Use Dify’s collaboration features to annotate or comment on model updates.

### Alternative: Dify Plugin
- Create a custom plugin to serve this documentation:
  - **manifest.yaml**:
    ```yaml
    name: model-documentation
    author: yourusername
    version: 1.0.0
    description: Documentation for multi-agent models
    ```
  - Host in a Git repository and install via Dify’s **Marketplace**.
  - Avoid `PluginDaemonBadRequestError` by ensuring unique `name`/`author` and clearing duplicates:
    ```
    rm -rf ~/dify/docker/plugins/yourusername_model-documentation
    ```

### Benefits of This Structure
- **Searchable**: Embedding models make it easy to find model details.
- **Collaborative**: Team members can update or query documentation.
- **Integrated**: Workflows enhance usability within Dify.
- **Versioned**: Git ensures trackable updates.
- **Secure**: Access control protects sensitive info.

## Testing Recommendations
- **Verify Models**:
  - Check Ollama:
    ```
    ollama list
    ```
  - Test in Dify workflows (e.g., image description with `llava`, image generation with `flux.1`).
- **Performance**:
  - Monitor RAM/GPU in Activity Monitor (total model size ~35GB).
  - Use lighter models (e.g., `phi3`) if 16GB RAM is strained.
- **Documentation Access**:
  - Search Knowledge Base for “llava use cases” to ensure retrieval works.
  - Test workflow responses for accuracy.

## Troubleshooting
- **Connection Issues**:
  - Ensure Ollama runs:
    ```
    ollama serve
    curl http://host.docker.internal:11434
    ```
  - Update `docker-compose.yaml` if needed:
    ```yaml
    services:
      dify-api:
        extra_hosts:
          - "host.docker.internal:host-gateway"
    ```
- **Plugin Errors**:
  - Check logs:
    ```
    docker logs dify-plugin-daemon-1
    ```
- **Storage**:
  - Verify space:
    ```
    df -h ~
    ```