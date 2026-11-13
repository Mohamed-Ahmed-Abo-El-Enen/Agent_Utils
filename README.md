# Agentic Utils

A collection of standalone Google Colab notebooks: agent studios and workflow platforms
(AutoGen Studio, Dify, Sim, Langflow, n8n), self-hosted agent gateways (OpenClaw, Hermes),
model-serving servers, GGUF conversion tooling, AI reverse-engineering and repo-wiki
generation, and LLM evaluation experiments. Every notebook in this
repo is built and tested to run on **Google Colab** — click the "Open In Colab" badge
under any notebook below to open it directly, fill in the settings cell(s), and run.

## Notebooks

### [`OpenSpec_Studio.ipynb`](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/OpenSpec_Studio.ipynb)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/OpenSpec_Studio.ipynb)
**What:** Spins up [OpenSpec](https://github.com/Fission-AI/OpenSpec) as a small web studio inside Colab, with a coding agent (Codex, Claude, Gemini, opencode, Cursor, GitHub Copilot, ...) wired in to work the spec.
**How:** Installs OpenSpec and the chosen agent CLI, writes a minimal `server.py` + static UI (`index.html`/`app.css`/`app.js`), starts the server, and exposes it publicly (e.g. via a tunnel) so you can create/open projects from the browser.
**Why:** Lets you drive an OpenSpec-based coding-agent workflow from a disposable Colab runtime instead of a local machine.
**Output:** A running studio UI at a public URL where projects are created and OpenSpec commands are executed through the selected agent.

### [`archify_studio_colab.ipynb`](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/archify_studio_colab.ipynb)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/archify_studio_colab.ipynb)
**What:** Runs [Archify](https://github.com/tt-a1i/archify) (a project-architecture visualizer/studio) on Colab and exposes it through a Cloudflare quick tunnel.
**How:** Step-by-step cells: clone & install Archify, install `cloudflared`, write the studio server and index page, write a sample project-architecture JSON, wire in an OpenAI key + private access key, start the server on port 8000, open the tunnel, verify the public link responds, then stop everything.
**Why:** Gives a shareable, temporary link to inspect/browse a project's architecture without any local setup.
**Output:** A public Cloudflare URL serving the Archify studio UI, plus a small JSON describing the sample project architecture.

### [`autogen_studio_colab_cloudflare.ipynb`](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/autogen_studio_colab_cloudflare.ipynb)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/autogen_studio_colab_cloudflare.ipynb)
**What:** Runs [AutoGen Studio](https://github.com/microsoft/autogen) on Colab against a **local model** (Ollama or vLLM — your choice per run) and exposes it through a Cloudflare tunnel.
**How:** Installs AutoGen Studio into its own uv venv plus nginx and `cloudflared`, starts the chosen model engine on the GPU, then fronts Studio with nginx behind an optional secret access key (the tunnel URL is public and Studio has no login of its own). Extra cells drive AutoGen from Python (a two-agent team with a tool on the local model), keep the runtime alive, and back up / restore the Studio database and team configs to Google Drive.
**Why:** A full multi-agent studio on free Colab hardware with no OpenAI key required, protected by an access key, and persistent across runtimes via Drive backups.
**Output:** A public (optionally key-gated) AutoGen Studio URL, plus `MyDrive/autogen-backup/autogen-data.tgz` when backed up.

### [`dify_colab_cloudflare.ipynb`](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/dify_colab_cloudflare.ipynb)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/dify_colab_cloudflare.ipynb)
**What:** Stands up a full [Dify](https://github.com/langgenius/dify) (LLM app platform) stack on a single Colab runtime — no Docker Compose — and exposes it via a Cloudflare tunnel.
**How:** Auto-detects the latest stable Dify tag, installs PostgreSQL 16 + pgvector, Redis, and nginx, builds the Dify API from source with uv, pulls the prebuilt web frontend straight out of the official Docker image with `crane` (falling back to a source build), wires everything together behind nginx, and opens the tunnel.
**Why:** Dify normally assumes Docker Compose, which Colab can't run; this reproduces the whole stack natively so you get a disposable, shareable Dify instance for free.
**Output:** A public URL serving the complete Dify console and API.

### [`sim_colab_cloudflare.ipynb`](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/sim_colab_cloudflare.ipynb)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/sim_colab_cloudflare.ipynb)
**What:** Runs [Sim](https://github.com/simstudioai/sim) (visual agent-workflow builder) on Colab with PostgreSQL 17, Redis, and nginx, exposed through a Cloudflare tunnel.
**How:** Resolves the requested Sim release from ghcr.io, installs and configures the database/cache/proxy stack, optionally starts a local model (Ollama or vLLM) on the GPU for Sim's agents to call, starts Sim behind the tunnel, and includes status/log, keep-alive, and Google Drive backup/restore cells.
**Why:** A disposable, shareable Sim instance — with optional fully local model serving — without Docker or any cloud account.
**Output:** A public URL serving the Sim studio, plus Drive backups of its data when requested.

### [`langflow_studio_colab.ipynb`](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/langflow_studio_colab.ipynb)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/langflow_studio_colab.ipynb)
**What:** Runs [Langflow](https://github.com/langflow-ai/langflow) on Colab with two model backends ready to use: a local Ollama model and an OpenAI-compatible hosted provider (Experiential Labs), exposed via a Cloudflare tunnel.
**How:** Installs Langflow into a uv venv, starts Ollama and pulls a model, verifies the hosted provider's key/models, launches Langflow with login enabled (superuser + password), registers a custom Langflow component for the hosted provider, and opens the tunnel to port 7860.
**Why:** A shareable Langflow studio where flows can mix free local models with a hosted API, with auth on so the public link isn't wide open.
**Output:** A public Langflow URL (login-protected) with both model providers available in the component library.

### [`n8n_studio_colab.ipynb`](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/n8n_studio_colab.ipynb)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/n8n_studio_colab.ipynb)
**What:** Runs [n8n](https://n8n.io) (workflow automation) v2 on Colab next to a local Ollama model, exposed via a Cloudflare tunnel.
**How:** Installs Node 22, n8n, Ollama, and `cloudflared`; starts Ollama (so n8n's AI nodes can call `localhost:11434`), starts n8n, opens the tunnel to port 5678, and includes commented-out cells to back up / restore n8n's data directory to Google Drive.
**Why:** A free, disposable n8n instance whose AI workflow nodes run against a local model instead of a paid API.
**Output:** A public n8n editor URL, with optional `MyDrive/n8n_backup/n8n_data.tgz` persistence.

### [`openclaw_agent_cloudflare.ipynb`](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/openclaw_agent_cloudflare.ipynb)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/openclaw_agent_cloudflare.ipynb)
**What:** Runs the [OpenClaw](https://openclaw.ai) agent gateway on Colab, backed by a local model (Ollama on T4, or vLLM on L4/A100), with its Control UI, a browser terminal, and optionally the raw model endpoint each on their own public Cloudflare link.
**How:** Starts the model backend with 64K context, installs Node 24 + OpenClaw + `cloudflared` + ttyd + tmux, configures OpenClaw to use the local model, starts the gateway, trusts the tunnel as a proxy, generates a one-time browser login link, and serves a tmux session over ttyd so you can drive OpenClaw from a terminal in any browser.
**Why:** A complete, self-hosted agent gateway — UI, API, and terminal — running on free GPU hardware with no API key spend.
**Output:** Public URLs for the Control UI (one-time login link), browser terminal, and optionally the model's OpenAI-compatible API, with all credentials printed in a summary cell.

### [`hermes_agent_cloudflare.ipynb`](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/hermes_agent_cloudflare.ipynb)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/hermes_agent_cloudflare.ipynb)
**What:** Runs Nous Research's [Hermes Agent](https://github.com/NousResearch/hermes-agent) on Colab against a local model (Ollama or vLLM, 64K context), exposing its OpenAI-compatible API, a Gradio chat UI, and a browser terminal on separate public Cloudflare links.
**How:** Starts the model backend, installs Hermes via its install script, points its config at the local model, starts the Hermes gateway on port 8642, tunnels it, smoke-tests the agent through the public API (it runs `nvidia-smi` on itself), then adds a login-protected Gradio chat and a ttyd/tmux terminal for the interactive `hermes` CLI.
**Why:** A tool-using agent you can reach three ways — API, chat UI, terminal — entirely self-hosted on a free Colab GPU.
**Output:** Public URLs + credentials for the Hermes API (`model: hermes-agent`), chat UI, and terminal.

### [`gitnexus_colab.ipynb`](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/gitnexus_colab.ipynb)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/gitnexus_colab.ipynb)
**What:** Generates an AI wiki for any git repository with [GitNexus](https://www.npmjs.com/package/gitnexus), using a local Ollama model, and serves the GitNexus web UI on a public Cloudflare link.
**How:** Installs Node 22 + GitNexus and Ollama, clones the target repo (including private Azure DevOps repos via org/project/PAT), runs `gitnexus wiki` pointed at the local model's OpenAI-compatible endpoint, then starts `gitnexus serve` + the web UI behind a bearer-token-protected tunnel.
**Why:** Repo documentation generated entirely on free hardware — the code and the model never leave the Colab runtime, which matters for private repos.
**Output:** A `.gitnexus/wiki` directory in the target repo and a token-protected public URL for browsing it.

### [`voice_studio_colab.ipynb`](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/voice_studio_colab.ipynb)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/voice_studio_colab.ipynb)
**What:** Runs [VoiceStudio](https://github.com/debpalash/VoiceStudio) (a local voice/TTS studio) on a Colab GPU and exposes it through a Cloudflare tunnel.
**How:** Clones the repo, builds the web UI with Bun (skipping the Electron binary — it runs headless), installs the Python backend with uv plus a cuDNN 8 compatibility shim for torch, starts the FastAPI backend with an auto-generated API key, and opens the tunnel; model weights and generated data can persist to Google Drive.
**Why:** GPU-accelerated voice generation in the browser with zero local setup, protected by an API key.
**Output:** A public VoiceStudio URL (plus its API key), with data optionally persisted under `MyDrive/VoiceStudio_data`.

### [`FreeToken_colab_server_L4.ipynb`](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/FreeToken_colab_server_L4.ipynb)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/FreeToken_colab_server_L4.ipynb)
**What:** Serves an LLM (default: `nvidia/Qwen3.6-35B-A3B-NVFP4`) via [FreeToken](https://github.com/) on a Colab GPU (needs sm_86+, i.e. L4/A100/RTX 30-40-50 class) and exposes an OpenAI-compatible endpoint.
**How:** Checks GPU compute capability, installs FreeToken + CUDA 13 libs + cloudflared, launches `ft serve` in the background with MoE slot sizing derived from available VRAM, waits for a real 1-token completion to confirm readiness, then opens a Cloudflare tunnel to the local server.
**Why:** Turns a free/cheap Colab GPU runtime into a temporary, internet-reachable OpenAI-compatible inference server for quick testing.
**Output:** A public URL (`PUBLIC_URL`) serving `/v1/chat/completions`, testable directly with the OpenAI Python client or `curl`.

### [`omniroute_colab_server.ipynb`](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/omniroute_colab_server.ipynb)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/omniroute_colab_server.ipynb)
**What:** Minimal launcher for the `omniroute` CLI server on Colab, exposed via a Cloudflare tunnel.
**How:** `npm install -g omniroute`, run it in the background with `nohup`, install `cloudflared`, then tunnel `localhost:20128` to a public URL.
**Why:** Quick way to get an Omniroute instance reachable from outside Colab with almost no setup.
**Output:** Log output confirming the server started, plus a public tunnel URL in `cloudflared.log`.

### [`Ollama_PublicURL.ipynb`](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/Ollama_PublicURL.ipynb)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/Ollama_PublicURL.ipynb)
**What:** Runs [Ollama](https://ollama.com) on a Colab GPU and exposes it through a public URL (Cloudflare tunnel or ngrok).
**How:** Installs Ollama and `cloudflared`, starts `ollama serve` in the background, pulls a chosen model (several presets commented out, e.g. `llama3.2:3b-instruct-fp16`, `qwen3:8b`, `gpt-oss:20b`), then opens either a Cloudflare quick tunnel or an ngrok tunnel (using an `NGROK_AUTHTOKEN` secret) to `localhost:11434`, and includes a small `query_ollama` helper plus a keep-alive loop.
**Why:** Gets a disposable, internet-reachable Ollama server running on free/cheap Colab GPU hardware for quick model testing.
**Output:** A public URL serving Ollama's `/api/chat` endpoint, plus a sample response printed from `query_ollama`.

### [`VLLM_Quantized_PublicURL.ipynb`](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/VLLM_Quantized_PublicURL.ipynb)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/VLLM_Quantized_PublicURL.ipynb)
**What:** Serves a quantized model (default: `IFM/K2-Horizon-7B`) with [vLLM](https://github.com/vllm-project/vllm) on Colab and exposes it via a Cloudflare tunnel.
**How:** Picks a dtype from the GPU's compute capability, launches `vllm serve` with tool-calling/reasoning parsers enabled, waits on `/health`, opens a Cloudflare tunnel, then drives the endpoint both with an async OpenAI client (streaming, bounded by a semaphore) and with a small `curl`+`jq` shell helper for concurrent prompts.
**Why:** Quick way to stand up and load-test an OpenAI-compatible vLLM server for a quantized model without local infrastructure.
**Output:** A public `/v1` endpoint, streamed completions for a batch of sample queries (printed and saved to `out.*.txt`), and `vllm.log`/`cf.log` for debugging.

### [`gguf_convert.ipynb`](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/gguf_convert.ipynb)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/gguf_convert.ipynb)
**What:** End-to-end GGUF conversion pipeline for diffusion/LLM checkpoints, built on `city96/ComfyUI-GGUF` and `llama.cpp`.
**How:** Fetches a checkpoint, detects its architecture (read live from ComfyUI-GGUF so new upstream families work without edits), figures out which tensors must stay F32 (including single-row parameters upstream's `n_dims == 1` rule misses), works out which quant targets are actually achievable given the source, converts, quantizes, and verifies the result against the original. Fill in settings 1a-1e and "Runtime → Run all"; a "survey a folder" mode can header-scan many checkpoints without downloading.
**Why:** Automates a fiddly, error-prone conversion process and avoids silently producing a broken or mis-typed GGUF.
**Output:** Converted/quantized `.gguf` file(s), a Markdown conversion report (architecture, source hash, F32-kept tensors, build settings), and optional upload of the result.

### [`llm_sglang_tpu.ipynb`](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/llm_sglang_tpu.ipynb)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/llm_sglang_tpu.ipynb)
**What:** Runs an LLM behind [SGLang](https://github.com/sgl-project/sglang)'s TPU backend on a Colab TPU runtime.
**How:** Detects the assigned TPU, installs SGLang's TPU backend, launches the server in the background, polls its health endpoint, talks to it with the OpenAI client, and optionally exposes it via a public URL — with cells to peek at server logs and cleanly stop everything.
**Why:** Validates that a model serves correctly on TPU hardware through an OpenAI-compatible API, without managing infrastructure by hand.
**Output:** A running local (and optionally public) OpenAI-compatible endpoint, plus a sample completion printed from the SGLang server.

### [`Rea_Reverse_engineering_MCP.ipynb`](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/Rea_Reverse_engineering_MCP.ipynb)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/Rea_Reverse_engineering_MCP.ipynb)
**What:** Reverse-engineers any software project — a GitHub URL, a Drive path, or an uploaded zip — by combining [REA](https://www.npmjs.com/package/rea-agents)'s static analysis with a GPT agent connected over **MCP**.
**How:** Installs Node 24 + REA, fetches the target, surveys its languages/manifests/artifacts, runs REA's static analysis on what it found, has GPT write a structured architecture report from the evidence, then starts REA's MCP server over stdio and wires it to a GPT tool-calling loop (runtime/execution tools filtered out by default) so you can interrogate the codebase interactively.
**Why:** Turns "what is this repo and how does it work?" into a one-click, evidence-grounded analysis — the agent cites REA's findings instead of guessing.
**Output:** A Markdown architecture report and a saved `transcript.md` of the full Q&A with the agent.

### [`harness2_discharge_assistant_colab.ipynb`](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/harness2_discharge_assistant_colab.ipynb)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/harness2_discharge_assistant_colab.ipynb)
**What:** A self-improving clinical discharge-summary anomaly detector running fully locally on Ollama, built around Google Research's [Harness2](https://github.com/google-research/harness2) recursive-refinement idea.
**How:** Defines an anomaly taxonomy (allergy conflicts, drug interactions, implausible doses, med discrepancies, contradictions, ...), runs a set of LLM detectors plus deterministic checks with strict evidence grounding (every finding must quote the record; drug-class facts verified against the NIH RxClass API), dedupes and verifies findings, then runs a Propose–Probe–Compose improvement loop that benchmarks candidate prompt harnesses on seeded anomalies and promotes only measured improvements — all behind a web app served over a Cloudflare tunnel.
**Why:** Explores whether a small local model with a carefully engineered, self-refining harness can do reliable clinical anomaly detection with zero data leaving the runtime.
**Output:** A public app URL for checking discharge summaries, plus the promoted harness, run logs, and benchmark scores saved to disk.

### [`jev_vs_openai_medical_anomaly.ipynb`](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/jev_vs_openai_medical_anomaly.ipynb)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/jev_vs_openai_medical_anomaly.ipynb)
**What:** Benchmarks three methods for flagging anomalies in medical discharge summaries: **Jev** (via OpenRouter's System One API), **GPT structured output**, and **GPT logprobs** (all OpenAI/OpenRouter-backed — no local model).
**How:** Loads discharge summaries from a CSV, asks the same shared question set of all three methods with matched concurrency and per-call timing, then compares them on a scoreboard (accuracy, ROC-AUC, Brier score, precision/recall/F1), plots (latency, calibration, agreement), a disagreement breakdown, and a stability check (repeated calls on a few cases).
**Why:** Answers whether a cheaper/self-reported probability method (structured JSON output) is as reliable as a measured one (logprobs) for this task, and how both compare to Jev.
**Output:** In-notebook scoreboard table, latency/calibration/agreement plots, and a list of cases where the methods disagree.

### [`laya_vs_jev_discharge_anomaly.ipynb`](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/laya_vs_jev_discharge_anomaly.ipynb)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/laya_vs_jev_discharge_anomaly.ipynb)
**What:** Benchmarks **Laya** (a local GPU classifier) against **Jev** (via OpenRouter) for detecting anomalies in discharge summaries.
**How:** Loads a discharge-summary CSV, chunks text for Laya (with configurable chunk size/overlap and checkpoint choice), runs both methods on every case with per-call timing, then produces a scoreboard, latency/calibration/agreement plots, a disagreement analysis, a confidence-gating pass (route low-confidence cases differently), and a stability check.
**Why:** Evaluates whether a local, self-hosted model (Laya) is a viable/cheaper substitute for a hosted model (Jev) on this classification task.
**Output:** `laya_vs_jev_*_results.csv`, `*_scoreboard.csv` saved to disk (and offered as a Colab download), plus in-notebook plots and disagreement/confidence-gating tables.

### [`laya_vs_jev_vs_gpt_discharge_anomaly.ipynb`](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/laya_vs_jev_vs_gpt_discharge_anomaly.ipynb)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/laya_vs_jev_vs_gpt_discharge_anomaly.ipynb)
**What:** Three-way extension of the above — **Laya** (local GPU) vs **Jev** (OpenRouter) vs **GPT-4o-mini**, the latter evaluated both via structured JSON output and via logprobs.
**How:** Same pipeline as `laya_vs_jev_discharge_anomaly.ipynb` (shared question design, CSV loading, shared answer parsing) extended with two GPT methods, run across all methods per case, then scored, plotted (latency, calibration, pairwise agreement), diffed for disagreements, confidence-gated, and stability-tested.
**Why:** A fuller comparison to see how a local model, a hosted specialist model, and a general-purpose frontier model trade off on accuracy, calibration, latency, and cost for medical anomaly detection.
**Output:** `laya_vs_jev_vs_gpt_results.csv`, `_scoreboard.csv`, and `_side_by_side.csv` saved to disk (and downloadable), plus in-notebook scoreboard, plots, and disagreement/confidence-gating analysis.

### [`zeek_vllm_qwen_langgraph_nsm.ipynb`](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/zeek_vllm_qwen_langgraph_nsm.ipynb)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/zeek_vllm_qwen_langgraph_nsm.ipynb)
**What:** A local AI network-security-monitoring pipeline: captures traffic, parses it with [Zeek](https://zeek.org), and has a [LangGraph](https://github.com/langchain-ai/langgraph) agent (backed by a self-hosted quantized Qwen via vLLM) triage and report on findings.
**How:** Installs Zeek + vLLM (Qwen2.5-7B-Instruct, AWQ/GPTQ/bnb/fp16 selectable), captures traffic (live interface, upload, or URL) into a pcap, runs Zeek offline to produce JSON logs, does deterministic pre-analysis/stats on those logs, defines a Pydantic schema for findings (severity/category/etc.), queries vLLM for structured output against that schema, and wires it all into a LangGraph pipeline with retries and checkpointing; a final cell repeats capture→analyze in rounds for continuous monitoring.
**Why:** Demonstrates an end-to-end, fully local/self-hosted alternative to cloud security-analysis tools — no traffic or logs leave the Colab runtime.
**Output:** `network_report.json` (structured, schema-validated findings per run) plus per-round reports from the continuous-monitoring loop.

### [`squash_commit_history.ipynb`](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/squash_commit_history.ipynb)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Mohamed-Ahmed-Abo-El-Enen/Agentic_Utils/blob/main/squash_commit_history.ipynb)
**What:** Squashes a Hugging Face Hub model repo's entire commit history into a single commit.
**How:** Authenticates with `HF_TOKEN` from Colab secrets, calls `HfApi.super_squash_history` on a given `REPO_ID`/branch, then lists the repo's commits to confirm the result.
**Why:** Cleans up bloated repo history (e.g. after many incremental pushes) without needing to clone/rewrite history locally.
**Output:** Confirmation message and the post-squash commit list for the target Hugging Face repo.
