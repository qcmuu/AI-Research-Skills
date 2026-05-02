---
  title: "Ollama"
  description: "Run large language models locally with a simple REST API and CLI. Supports Llama, Mistral, Gemma, Qwen, DeepSeek, and 100+ models. Zero-config setup, model library, multimodal support, and OpenAI-compatible API. Best for local development, offline inference, and privacy-sensitive workloads."
  skillName: "ollama"
  skillVersion: "1.0.0"
  skillAuthor: "Orchestra Research"
  skillLicense: "MIT"
  skillTags: ["Inference", "Ollama", "Local LLMs", "REST API", "OpenAI Compatible", "Privacy", "Offline", "Llama", "Mistral", "Gemma"]
  skillDeps: ["ollama", "httpx", "openai"]
  ---

  | | |
  |---|---|
  | **Version** | 1.0.0 |
  | **Author** | Orchestra Research |
  | **License** | MIT |
  | **Tags** | `Inference` `Ollama` `Local LLMs` `REST API` `OpenAI Compatible` `Privacy` `Offline` |
  | **Dependencies** | `ollama` `httpx` `openai` |


  # Ollama — Run LLMs Locally

  The simplest way to run open-source LLMs on your own hardware.

  ## When to use Ollama

  **Use Ollama when:**
  - Local development without cloud API costs
  - Privacy-sensitive workloads (data never leaves your machine)
  - Offline inference required
  - Rapid prototyping with 100+ available models
  - OpenAI API drop-in replacement needed

  **Metrics**:
  - **100,000+ GitHub stars**
  - **100+ supported models** (Llama 3, Mistral, Gemma, Qwen, DeepSeek, Phi)
  - **Zero-config setup** — single binary

  ## Quick start

  ```bash
  curl -fsSL https://ollama.com/install.sh | sh
  ollama pull llama3.2
  ollama run llama3.2
  ```

  ### Python SDK

  ```python
  import ollama

  response = ollama.chat(
      model='llama3.2',
      messages=[{'role': 'user', 'content': 'What is GRPO training?'}]
  )
  print(response['message']['content'])

  # Streaming
  for chunk in ollama.generate(model='llama3.2', prompt='Explain LoRA', stream=True):
      print(chunk['response'], end='', flush=True)
  ```

  ### OpenAI-compatible drop-in

  ```python
  from openai import OpenAI
  client = OpenAI(base_url='http://localhost:11434/v1', api_key='ollama')
  response = client.chat.completions.create(
      model='llama3.2',
      messages=[{'role': 'user', 'content': 'Explain attention mechanisms'}]
  )
  ```

  ### Embeddings for RAG

  ```python
  import ollama
  response = ollama.embeddings(model='nomic-embed-text', prompt='Flash Attention paper')
  embedding = response['embedding']  # 768-dim vector
  ```

  ### Custom Modelfile

  ```dockerfile
  FROM llama3.2
  SYSTEM "You are an expert AI researcher. Provide precise, citation-backed answers."
  PARAMETER temperature 0.2
  PARAMETER num_ctx 8192
  ```

  ```bash
  ollama create research-assistant -f Modelfile
  ollama run research-assistant
  ```

  ## Model library

  | Model | Size | Best for |
  |-------|------|----------|
  | llama3.2 | 3B, 8B | General purpose |
  | llama3.1:70b | 70B | High quality |
  | mistral | 7B | Instruction following |
  | qwen2.5-coder | 7B, 32B | Code generation |
  | deepseek-r1 | 8B–70B | Reasoning |
  | phi4 | 14B | Compact + capable |
  | llava | 7B, 13B | Vision + language |

  ## REST API

  ```bash
  curl http://localhost:11434/api/generate -d '{"model":"llama3.2","prompt":"Explain FSDP","stream":false}'
  ```

  ## References
  - [Ollama GitHub](https://github.com/ollama/ollama)
  - [Model Library](https://ollama.com/library)
  - [API Reference](https://github.com/ollama/ollama/blob/main/docs/api.md)
  