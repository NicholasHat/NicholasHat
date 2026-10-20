# Nicholas Tweedie

I'm a Software Engineering student at UC Irvine (B.S. expected June 2028). I've been fascinated by technology since long before college, and what keeps me building is the number of real problems software can solve. Lately most of my work has been on running LLMs on-device, local-first AI tools, and data pipelines that turn research papers into something a lab can actually query.

I currently work as a Software Developer (Undergraduate Researcher) at the Zenyuk Lab at UCI's National Fuel Cell Research Center, and I'm looking for a Software Engineering internship for Summer 2027.

## Projects

### [ZeroHop](https://github.com/NicholasHat/ZeroHop)
Swift, Python, Core ML, MLX, Metal

Speculative decoding across the Apple Neural Engine and the GPU on a single M3, using public APIs only. A 1B draft model runs on the ANE while an 8B target verifies on the GPU. I measured a 1.47x decoding speedup over a GPU-only baseline with token-exact output, and the ANE draft is fully hidden inside the GPU's verify window. On my M3 that's 28.1 tok/s vs 19.1 with greedy decoding. Before writing any model code I built a zero-allocation measurement harness with a kill criterion for the ANE-to-GPU handoff. It traced the handoff's latency tail to the GPU dropping its clock when idle, which isn't in Apple's documentation. Keeping the GPU busy takes p99 handoff latency from 1.33 ms to 165 µs, about three orders of magnitude below the compute on either side. Getting a stateful KV-cache Llama onto the ANE meant working through four toolchain failures. One was a silent tracing bug that left the output correct but held draft acceptance at 11%. Fixing it raised acceptance to 50% against a 3B target, and the fixed draft reaches 86% against the 8B.

### [oss-instruct-py](https://github.com/NicholasHat/oss-instruct-py)
Python, MLX, Hugging Face, Anthropic Batches API

The OSS-Instruct method from the Magicoder paper, adapted to run end to end on Apple Silicon. I generated about 30K synthetic instruction/solution pairs from open-source code with the Anthropic Batches API, kept about 28K for training after filtering and dedup, LoRA fine-tuned Qwen2.5-Coder-3B-Instruct with mlx-lm, and evaluated on HumanEval and MBPP under the same greedy protocol for both arms. HumanEval pass@1 went from 67.7% to 70.7% and MBPP from 58.2% to 59.6%. The tuned adapter is on [Hugging Face](https://huggingface.co/nicholashat/qwen2.5-coder-3b-oss-instruct-lora). A 7B run kept hitting a deterministic NaN. An A/B repro script traced it to MLX corrupting buffers past its wired-memory limit, not to the training config. Gradient checkpointing cut peak step memory from 13.4 GB to 6.6 GB and ran clean through a 1,200-iteration diagnostic. The full 7B run is still in progress.

### [project-steward](https://github.com/NicholasHat/project-steward) (Project Truth Engine)
Python, FastAPI, PostgreSQL/pgvector, React, Docker

Point it at a messy folder of project files and it reconstructs what happened, in what order, what's missing, and where the project drifted from its original direction. Every inference carries its evidence back to the source files. It's an 11-stage pipeline (ingest through report) that parses six formats: PDF, Word, PowerPoint, spreadsheets, images and text. A React dashboard sits on top, and the backend deploys with one `docker compose up` (FastAPI, Postgres with pgvector, Ollama, and Caddy with automatic HTTPS). Structured data, the relationship graph, and embeddings all live in one Postgres store, so there's no separate vector database. On startup, a reconciliation sweep marks runs orphaned by a crash as failed so they don't block new ones. CI runs the 213-test suite against a fresh pgvector database on every push to main and every PR.

### [rare-earth-extraction](https://github.com/NicholasHat/rare-earth-extraction)
Python, Anthropic Claude, Streamlit, SQLite, pdfplumber

Built for a UCI chemistry lab with thousands of papers and no machine-readable data. A versioned Claude extraction pipeline digitizes extraction-vs-pH figures out of research PDFs. To catch the model silently dropping points, a deterministic pdfplumber pass reads markers and calibrates axes straight from the PDF's vector geometry, then hands the model those coordinates as anchors. On the reference paper, automatic axis calibration went from 0 of 10 axes to 9 of 10. The first real paper the hand-off ran on came out with a median error of 0.01 %E across 171 points against the human-approved data. Every extraction goes through an automatic QA suite and human review before it's merged, in one atomic transaction with an audit log. The assistant that answers questions over the data has read-only access, so it can't change anything even if someone jailbreaks it. 330 tests run offline.

### [rate-limiter](https://github.com/NicholasHat/rate-limiter)
Python, Terraform, AWS Lambda, API Gateway, DynamoDB, k6

Three rate limiters (a naive token bucket, an atomic token bucket, and a sliding window) deployed as parallel Lambda routes from one Terraform map, then load-tested with identical k6 bursts of 100 requests from 10 concurrent workers. With a limit of 10, the non-atomic version admitted 35, because concurrent reads saw stale state. A DynamoDB conditional-write compare-and-set brought that to 11, consistent with one token refilling during the 1.5 s burst. The sliding window admitted exactly 10. Correctness has a cost: p99 latency rose from 163 ms to about 380 ms on the atomic paths. There's also a CAS retry and jittered-backoff experiment, plus GitHub Actions CI for the Terraform checks and unit tests.

### [local-AI](https://github.com/NicholasHat/local-AI)
Python, FastAPI, React/TypeScript, Ollama, ChromaDB

A ChatGPT-style assistant that runs entirely on your own machine through Ollama. I built it to understand how modern agents actually work: a real function-calling loop, document RAG, PDF form filling, a file-based skills system the model can extend, and a coding agent that works in a throwaway git worktree, so nothing lands until a human approves the full diff. The model can write new skills for itself, but only as instruction files, never executable ones, so a prompt injection can't plant code as a skill. 320+ tests run without a live model by routing every LLM call through one mockable client.

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
