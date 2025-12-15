---
title: "Self-host Sim in minutes"
description: "Launch the Sim workflow builder locally with npm or Docker, including options for Ollama and vLLM."
pubDate: 2025-02-24
heroImage: "/blog-placeholder-5.jpg"
---

Sim ships with a fully hosted experience at [sim.ai](https://sim.ai), but you can also run it yourself when you need extra control over infrastructure or data residency. Here are the quickest ways to get going.

## One-line npm setup

The fastest local start uses the published npm package. Make sure Docker is running, then execute:

```bash
npx simstudio
```

By default Sim serves the canvas at <http://localhost:3000>. Use `-p`/`--port` to override the port and `--no-pull` if you want to skip pulling the latest Docker images before launch.

## Docker Compose

If you want to clone the repository and run with a compose stack, use:

```bash
git clone https://github.com/simstudioai/sim.git
cd sim
docker compose -f docker-compose.prod.yml up -d
```

Then open <http://localhost:3000/>. If you prefer local models, swap to the Ollama profiles:

```bash
# GPU profile (downloads gemma3:4b automatically)
docker compose -f docker-compose.ollama.yml --profile setup up -d

# CPU-only profile
docker compose -f docker-compose.ollama.yml --profile cpu --profile setup up -d
```

When Ollama runs outside of Docker, set `OLLAMA_URL` to use `host.docker.internal` (or your host IP on Linux) so the Sim containers can reach it.

## vLLM endpoints

Sim also supports OpenAI-compatible [vLLM](https://docs.vllm.ai/) servers. Provide your base URL and optional API key via environment variables:

```bash
VLLM_BASE_URL=http://your-vllm-server:8000
VLLM_API_KEY=your_optional_api_key
```

Use `host.docker.internal` if the vLLM server runs on your host machine; otherwise, point to any accessible address.
