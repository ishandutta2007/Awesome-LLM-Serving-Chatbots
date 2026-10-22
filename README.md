# Awesome-LLM-Serving-Chatbots

# Top LLM Serving & Chatbots Ecosystem

**Curated List of SaaS Products & Open-Source GitHub Projects**  
*Focused on High-Throughput Inference, Self-Hosted Serving Engines & Chatbot Frameworks*  
**Last updated: October 2026**

This repository tracks notable **SaaS platforms** and **open-source projects** for **LLM Serving & Chatbots**. These tools enable teams to deploy language models behind APIs, manage inference infrastructure, and build conversational interfaces—ranging from managed endpoints that abstract away GPUs to open-source serving engines that squeeze maximum throughput from your own hardware.

**Examples** include Hugging Face Inference Endpoints, Replicate, Together AI, Anyscale, DeepInfra, Baseten, RunPod, Modal, and vLLM (the category leaders).

**Open-source emphasis**: This section is heavily expanded with every major active project for self-hosting, avoiding per-token vendor lock-in, and controlling your inference stack—ideal for teams that need data sovereignty, predictable costs, or the ability to fine-tune serving behavior. The open-source landscape is anchored by **vLLM** (the PagedAttention standard with the broadest model support), **SGLang** (the structured generation specialist with RadixAttention), and **Hugging Face TGI** (the production-grade Rust server), with **FastChat** serving as the reference chatbot platform from LMSYS and **Ollama** providing the simplest local deployment path.

Contributions welcome! Open a PR to add/update entries. Keep descriptions factual and link to official sites.

## Table of Contents
- [SaaS/Hosted Platforms](#saas-hosted-platforms)
- [Open-Source GitHub Projects](#open-source-github-projects)
- [How to Contribute](#how-to-contribute)
- [Disclaimer](#disclaimer)

## SaaS/Hosted Platforms

- **[Hugging Face Inference Endpoints](https://huggingface.co/inference-endpoints)**  
  Dedicated endpoints for any Hugging Face model, billed per-minute while the endpoint is running. **GPU pricing**: T4 $0.50/hr, L4 $0.80/hr, A10G $1.00/hr, L40S $1.80/hr, A100 80GB $2.50/hr . Best for teams already in the Hugging Face ecosystem that want a straightforward path from model hub to production endpoint.

- **[Replicate](https://replicate.com/)**  
  Pay-per-second inference platform with a vast model catalog. Pricing varies by hardware, starting from $0.0002–$0.01/second; new accounts get $25 in free credit . Best for experimentation and running community models without managing infrastructure.

- **[Together AI](https://www.together.ai/)**  
  Offers both serverless (per-token) and **dedicated endpoints** (per-minute). **Dedicated GPU rates**: H100 80GB $5.49/hr, B200 180GB $8.99/hr; H200 and GB300 are contact-sales. Billing is per ready replica per minute—provisioning and cold-start time are not billed . Best for teams that want to graduate from serverless to reserved capacity as volume grows.

- **[Anyscale](https://www.anyscale.com/)**  
  Managed Ray platform with pay-as-you-go compute. **Instance rates**: T4 $0.5682/hr, L4 $0.9542/hr, A10G $1.3635/hr, A100 $4.9591/hr; H/B/GB families are quote-based. New accounts get $100 in credits . Best for teams already using Ray for distributed training or batch inference that want a unified serving layer.

- **[DeepInfra](https://deepinfra.com/)**  
  Per-token inference provider with transparent pricing and cached-token discounts. Example: DeepSeek-V4-Pro at $1.30/M input and $2.60/M output, with cached input at $0.10/M—significantly cheaper than Azure for equivalent workloads . SOC 2 and ISO 27001 certified. Best for cost-sensitive production workloads with predictable token volumes.

- **[Baseten](https://www.baseten.co/)**  
  Model serving platform with **cache token pricing** introduced April 2026—cached input tokens are billed at a discounted rate automatically, benefiting agentic workloads with high cache hit rates . Best for teams serving agent workloads where system prompts and tool schemas are reused across requests.

- **[RunPod](https://www.runpod.io/)**  
  Serverless GPU platform with **per-second billing**. **Flex workers** scale to zero for variable workloads; **Active workers** run 24/7 with sales-negotiated discounts. Billed for cold start, execution, and idle timeout (default 5 seconds). Storage: container disk ~$0.10/GB/month, network volume $0.07/GB/month (<1TB) . Best for developers who want per-second economics and SDK-first control.

- **[Modal](https://modal.com/)**  
  Serverless compute platform for AI workloads. **Starting October 1, 2026, network egress is billed**: Starter includes 1 TiB/month, Team 10 TiB, Enterprise 100 TiB; overage at $0.04/GiB . Best for teams already using Modal for batch jobs and functions that want to consolidate serving on the same platform.

- **[Lepton AI](https://www.lepton.ai/)**  
  Serverless inference with per-token pricing (e.g., Mixtral 8x7B at $0.50/M tokens) and rate limits on the Basic plan . Best for simple, low-volume inference where per-token pricing is sufficient.

- **Note on OctoAI**: OctoAI has been discontinued; do not select it for new deployments .

## Open-Source GitHub Projects

- **[vLLM](https://github.com/vllm-project/vllm)**  
  **The PagedAttention standard.** Originally from UC Berkeley's Sky Computing Lab, now with 2,000+ contributors. **Key innovations**: PagedAttention for efficient KV-cache memory management, continuous batching, chunked prefill, prefix caching, speculative decoding, and multi-LoRA support. **Model coverage**: 200+ architectures including decoder-only (Llama, Qwen, Gemma), MoE (Mixtral, DeepSeek-V3), hybrid attention (Mamba), multimodal (LLaVA, Qwen-VL), and embedding models. **Hardware**: NVIDIA, AMD, Intel GPUs, plus TPU, Gaudi, and Apple Silicon plugins. **OpenAI-compatible API server** plus Anthropic Messages API and gRPC support . Best for production serving where you want the broadest model support and active community development.

- **[SGLang](https://github.com/sgl-project/sglang)**  
  **The structured generation specialist.** Features **RadixAttention** for efficient prefix caching across requests and **compressed finite state machines** for fast structured output (JSON schemas, regex constraints). **Performance**: demonstrated 25x inference speedup on NVIDIA GB300 NVL72; 3.8x prefill and 4.8x decode throughput for DeepSeek on GB200 NVL72 . Day-0 support for new open models (MiMo-V2-Flash, Mistral Large 3, DeepSeek-V3.2). **Strengths**: best-in-class for multi-turn conversations, agent workflows, and structured output where prefix reuse is high. Best for teams building chatbots or agents where KV-cache reuse and constrained generation are critical.

- **[Hugging Face TGI (Text Generation Inference)](https://github.com/huggingface/text-generation-inference)**  
  **The production-grade Rust server.** Features: token streaming via SSE, continuous batching, **speculative decoding** (~2x latency improvement), **guidance/JSON** for structured output, and fine-tuned model support. **Hardware**: NVIDIA, AMD (ROCm), Intel GPU, Gaudi, Inferentia, and Google TPU. Ships as a Docker container with an **OpenAI Chat Completion compatible Messages API** . Best for teams in the Hugging Face ecosystem that want a battle-tested, Docker-native serving solution with strong observability.

- **[FastChat](https://github.com/lm-sys/FastChat)**  
  **The reference chatbot platform from LMSYS.** Provides the complete stack for training, serving, and evaluating chatbots: **controller** for coordinating workers, **model workers** for hosting models, and a **Gradio web UI** for interaction. Supports model parallelism across GPUs, 8-bit compression (`--load-8bit`), CPU offloading, and Metal backend for Apple Silicon. **Vicuna-13B with 8-bit compression runs on a single 16GB GPU** (3090/4080/T4/V100) . Best for researchers and teams that want an end-to-end chatbot reference implementation, not just an inference engine.

- **[Ollama](https://github.com/ollama/ollama)**  
  **The simplest local deployment.** 182K+ GitHub stars, Go-based, MIT licensed. One-command model pull and run (`ollama run llama3`). Manages model weights, GPU layers, and context automatically. **Strengths**: lowest barrier to entry for local LLM serving; OpenAI-compatible API. **Limitations**: less optimized for high-concurrency production serving than vLLM or SGLang; single-user focus. Best for local development, prototyping, and single-user chatbot deployments .

### Additional Strong Open-Source Options

- **llama.cpp** — The C/C++ inference engine underpinning many local tools. Best for CPU/GPU inference on edge hardware.
- **LMDeploy** — InternVL's serving toolkit with TurboMind engine. Best for multimodal model serving.
- **OpenLLM (BentoML)** — Production serving with built-in observability and adaptive batching. Best for teams already using BentoML for model packaging.
- **Frameworks for building custom systems**: Use **vLLM** as the general-purpose serving backbone. Add **SGLang** when structured output or agent workloads dominate. Use **TGI** if you want a Docker-native Hugging Face solution. Use **FastChat** as a reference for chatbot-specific architecture. Use **Ollama** for local development and **vLLM** for production.

## How to Contribute

1. Fork the repo.
2. Add/edit entries in `README.md` (follow existing format).
3. Include: name, link, 1–2 sentence description, and whether it's SaaS or open-source.
4. Submit PR with a short explanation.

Star the repo if you find it useful!

## Disclaimer

- This is a **community-curated** list — not exhaustive and not an endorsement.
- **Managed vs. self-hosted economics differ dramatically**: Together AI's dedicated H100 at $5.49/hr costs ~$3,950/month if running continuously, versus serverless per-token pricing that scales with actual usage . Model your traffic pattern before committing to reserved capacity.
- **OctoAI is discontinued**: do not evaluate it for new projects .
- **Modal now charges for egress** (starting October 2026), which can affect workloads that stream large responses or transfer data out .
- **Self-hosted serving requires GPU operations expertise**: vLLM, SGLang, and TGI all assume you can manage CUDA drivers, model weights, and scaling. Ollama lowers this barrier but trades away production throughput.

---

**Made for ML engineers, platform teams, and developers deploying LLM-powered chatbots.**  
Let's make LLM serving more open, throughput-efficient, and appropriately scoped.
