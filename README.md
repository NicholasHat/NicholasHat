# Nicholas Tweedie

I'm a Software Engineering student at UC Irvine (B.S. expected June 2028). I've been fascinated by technology since long before college, and what keeps me building is the number of real problems software can solve. Lately most of my work has been on running LLMs on-device, local-first AI tools, and data pipelines that turn research papers into something a lab can actually query.

I currently work as a Software Engineer at the Zenyuk Lab at UCI's National Fuel Cell Research Center, and I'm looking for a Software Engineering internship for Summer 2027.

## Projects

### [ZeroHop](https://github.com/NicholasHat/ZeroHop)
Swift, Python, Core ML, MLX, Metal

Speculative decoding across the Apple Neural Engine and the GPU on a single M3, using public APIs only. A 1B draft model runs on the ANE while an 8B target verifies on the GPU. I measured a 1.47x decoding speedup over a GPU-only baseline with token-exact output, and the ANE draft is fully hidden inside the GPU's verify window. Before writing any model code I built a measurement harness with a kill criterion for the ANE-to-GPU handoff; it brought p99 handoff latency from 1.33 ms down to 165 us once I found two power-state effects that aren't in Apple's documentation. Getting a stateful KV-cache Llama onto the ANE meant working through four toolchain failures, including a silent tracing bug that capped draft acceptance at 11% (now 86%).

### [oss-instruct-py](https://github.com/NicholasHat/oss-instruct-py)
Python, MLX, Hugging Face, Anthropic Batches API

A reproduction of the OSS-Instruct method from the Magicoder paper, rebuilt for Apple Silicon. I generated about 28K synthetic instruction/solution pairs from open-source code, LoRA fine-tuned Qwen2.5-Coder-3B with mlx-lm, and evaluated on HumanEval and MBPP under the same greedy protocol for both arms. HumanEval pass@1 went from 67.7% to 70.7% and MBPP from 58.2% to 59.6%. The tuned adapter is on [Hugging Face](https://huggingface.co/nicholashat/qwen2.5-coder-3b-oss-instruct-lora). A 7B run kept hitting a deterministic NaN that I traced to MLX wired-memory-limit buffer corruption rather than anything in the training config, with an A/B repro script to prove it.

### [project-steward](https://github.com/NicholasHat/project-steward) (Project Truth Engine)
Python, FastAPI, PostgreSQL/pgvector, React, Docker

Point it at a messy folder of project files and it reconstructs what happened, in what order, what's missing, and where the project drifted from its original direction. Every inferred fact traces back to the source files. It's an 11-stage pipeline behind a React dashboard that deploys with one `docker compose up` (FastAPI, Postgres with pgvector, Caddy for HTTPS). Structured data, the relationship graph, and embeddings all live in one Postgres store, so there's no separate vector database. A reconciliation sweep on startup recovers background jobs left orphaned by worker crashes, and CI runs the test suite against a fresh database on every push.

### [rare-earth-extraction](https://github.com/NicholasHat/rare-earth-extraction)
Python, Anthropic Claude, Streamlit, SQLite, pdfplumber

Built for a UCI chemistry lab with thousands of papers and no machine-readable data. A versioned Claude extraction pipeline digitizes extraction-vs-pH figures out of research PDFs. To catch the model silently dropping points, a deterministic pass counts figure markers straight from the PDF's vector geometry and feeds that back as ground truth. Every extraction goes through an automatic QA suite and human review before it's merged, in one atomic transaction with an audit log. The assistant that answers questions over the data has read-only access, so it can't change anything even if someone jailbreaks it.

### [rate-limiter](https://github.com/NicholasHat/rate-limiter)
Python, Terraform, AWS Lambda, API Gateway, DynamoDB, k6

Three rate limiters (a naive token bucket, an atomic token bucket, and a sliding window) deployed as parallel Lambda routes from one Terraform map, then load-tested with identical k6 bursts. With a limit of 10, the non-atomic version admitted 35 of 100 requests. A DynamoDB conditional-write compare-and-set brought that to 11, and the sliding window admitted exactly 10. There's also a CAS retry and jittered-backoff experiment, plus GitHub Actions CI for the Terraform checks and unit tests.

### [local-AI](https://github.com/NicholasHat/local-AI)
Python, FastAPI, React/TypeScript, Ollama, ChromaDB

A ChatGPT-style assistant that runs entirely on your own machine through Ollama. I built it to understand how modern agents actually work: a real function-calling loop, document RAG, PDF form filling, a file-based skills system the model can extend, and a coding agent that edits local repos with human approval on every change. The model can write new skills for itself, but only as instruction files, never executable code, which closes off prompt injection turning into code execution. 180+ tests run without a live model by routing every LLM call through one mockable client.

## Other work

At the Zenyuk Lab I built the extraction pipeline above and shipped the Streamlit app the lab uses to run it: batch PDF ingestion, a review queue, and a tool-calling lab assistant with guarded SQL access, backed by 125+ tests. Before that I was on a 3-person team building NIMBUS, a real-time ASL interpretation system, where I wrote the serverless AWS backend and a WebSocket ingestion layer streaming 258 MediaPipe keypoints at 10 FPS. I frequently attend hackathons to push myself to learn new technologies.

## Skills

| | |
| :--- | :--- |
| **Languages** | Python, TypeScript, JavaScript, Swift, C/C++, SQL, Java |
| **AI / ML** | Core ML, MLX, LoRA fine-tuning (mlx-lm), Hugging Face, Ollama, Anthropic Claude API, AWS Bedrock, LLM tool-calling and RAG, NumPy, Pandas |
| **Backend and cloud** | FastAPI, PostgreSQL/pgvector, SQLite, AWS (Lambda, API Gateway, DynamoDB, S3, Polly, Rekognition), Docker, Terraform, AWS SAM, GitHub Actions, k6 |
| **Frontend** | Next.js, React, TailwindCSS, Streamlit, Three.js |

## Contact

- LinkedIn: [linkedin.com/in/nicholas-tweedie-425a9b32b](https://linkedin.com/in/nicholas-tweedie-425a9b32b)
- Hugging Face: [huggingface.co/nicholashat](https://huggingface.co/nicholashat)
- Email: [ntweedie@uci.edu](mailto:ntweedie@uci.edu)
