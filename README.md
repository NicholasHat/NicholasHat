# Hi, I'm Nicholas Tweedie 👋

Software Engineering student at the **University of California, Irvine** (B.S. expected June 2028). I build systems-level AI software: on-device LLM inference, local-first AI tooling, and LLM data pipelines that are QA-gated and auditable. Currently an undergraduate researcher at the **Zenyuk Lab, National Fuel Cell Research Center**.

**Open to Summer 2027 software engineering internships** — especially inference, ML infrastructure, and backend roles.

---

## 🚀 Featured Projects

### ⚡ [ZeroHop](https://github.com/NicholasHat/ZeroHop) — speculative decoding across the Apple Neural Engine and GPU
*Swift, Python, Core ML, MLX, Metal*

A 1B draft model runs on the ANE while an 8B target verifies on the GPU, on one consumer M3 chip using public APIs only. **1.47× decoding throughput** over a GPU-only baseline, token-exact output, and the ANE draft fully hidden inside the GPU's verify window. A zero-alloc measurement harness (10k-iteration protocol, p50/p95/p99/p99.9) cut ANE→GPU handoff tail latency from **p99 1.33 ms to 165 µs** by isolating two undocumented power-state effects. Getting a stateful KV-cache Llama onto the ANE took resolving four toolchain walls, including a silent tracing bug that capped draft acceptance at 11% (now 86%).

### 🧬 [oss-instruct-py](https://github.com/NicholasHat/oss-instruct-py) — fine-tuning a code LLM with OSS-Instruct on Apple Silicon
*Python, MLX, Hugging Face, Anthropic Batches API* · [tuned adapter on Hugging Face](https://huggingface.co/nicholashat/qwen2.5-coder-3b-oss-instruct-lora)

End-to-end reproduction of the Magicoder OSS-Instruct method: ~28K synthetic instruction/solution pairs generated from The Stack, LoRA fine-tuning of Qwen2.5-Coder-3B via `mlx-lm`, HumanEval/MBPP evaluation. **HumanEval pass@1 67.7% → 70.7%**, MBPP 58.2% → 59.6%, same greedy protocol both arms. Also root-caused a deterministic NaN in a 7B run to MLX wired-memory-limit buffer corruption (not hyperparameters), with an A/B repro script.

### 🗂️ [project-steward](https://github.com/NicholasHat/project-steward) — Project Truth Engine
*Python, FastAPI, PostgreSQL/pgvector, React, Docker*

Point it at a messy folder of project files and it reconstructs the timeline, flags gaps, and labels drift, with every inferred fact traced back to source artifacts. An 11-stage pipeline behind a React dashboard, one `docker compose up` to deploy (FastAPI, Postgres + pgvector, Caddy auto-HTTPS). Structured data, relationship graph, and embeddings live in a single Postgres store. A startup reconciliation sweep recovers background jobs orphaned by worker crashes; CI runs the suite against a fresh database.

### 🔬 [rare-earth-extraction](https://github.com/NicholasHat/rare-earth-extraction) — research papers → queryable REE database
*Python, Anthropic Claude, Streamlit, SQLite, pdfplumber*

Built for a UCI chemistry lab. A versioned Claude extraction pipeline digitizes % Extraction vs. pH figures from research PDFs, grounded against a deterministic vector-geometry marker count that catches silent under-digitization. Every extraction passes an automatic QA suite and human review before merge, in one atomic transaction with an audit log. The query-facing assistant has a strict read-only boundary, so it cannot mutate data even if jailbroken.

### 🚦 [rate-limiter](https://github.com/NicholasHat/rate-limiter) — three distributed rate limiters, load-tested side by side
*Python, Terraform, AWS Lambda / API Gateway / DynamoDB, k6*

Naive token bucket, atomic token bucket, and sliding window deployed as parallel Lambda routes from one Terraform map, then hit with identical k6 bursts. The non-atomic version admitted **35 of 100** requests against a limit of 10; a DynamoDB conditional-write compare-and-set cut that to 11, and the sliding window to exactly 10. Includes a CAS retry/jittered-backoff experiment and GitHub Actions CI for Terraform checks and unit tests.

### 🤖 [local-AI](https://github.com/NicholasHat/local-AI) — private AI assistant with tool use, RAG, and a sandboxed coding agent
*Python, FastAPI, React/TypeScript, Ollama, ChromaDB*

A ChatGPT-style assistant that runs entirely on-device via Ollama: real function-calling agent loop, document RAG, PDF form filling, a file-based skills system the model can extend, and a coding agent that edits local repos under human approval. Prompt-injection-to-code-execution is closed by design (self-authored skills are instruction files only). 180+ tests with no live-model dependency, via a single mockable client seam.

---

## 🛠️ Tech Stack

| Category | Technologies |
| :--- | :--- |
| **Languages** | Python, TypeScript, JavaScript, Swift, C/C++, SQL, Java |
| **AI & ML** | Core ML, MLX, LoRA fine-tuning (`mlx-lm`), Hugging Face, Ollama, Anthropic Claude API, AWS Bedrock, LLM tool-calling & RAG, NumPy, Pandas |
| **Backend & Cloud** | FastAPI, PostgreSQL/pgvector, SQLite, AWS (Lambda, API Gateway, DynamoDB, S3, Polly, Rekognition), Docker, Terraform, AWS SAM, GitHub Actions, k6 |
| **Frontend** | Next.js, React, TailwindCSS, Streamlit, Three.js |

---

## 📊 GitHub Metrics

<p align="left">
  <img src="https://github-stats-extended.vercel.app/api?username=NicholasHat&show_icons=true&theme=tokyonight" alt="Nicholas's GitHub Stats" height="180px"/>
  <img src="https://github-stats-extended.vercel.app/api/top-langs/?username=NicholasHat&layout=compact&theme=tokyonight" alt="Top Languages" height="180px"/>
</p>

---

## 🤝 Connect with Me

* **LinkedIn:** [linkedin.com/in/nicholas-tweedie-425a9b32b](https://linkedin.com/in/nicholas-tweedie-425a9b32b)
* **Hugging Face:** [huggingface.co/nicholashat](https://huggingface.co/nicholashat)
* **Email:** [ntweedie@uci.edu](mailto:ntweedie@uci.edu) · [nttweedie@gmail.com](mailto:nttweedie@gmail.com)
