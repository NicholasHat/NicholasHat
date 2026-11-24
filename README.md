<h1 align="center">Nicholas Tweedie</h1>

<p align="center">
  Software Engineering @ UC Irvine | Undergraduate Researcher, Software @ National Fuel Cell Research Center
</p>

<p align="center">
  <a href="https://www.linkedin.com/in/nicholas-tweedie/"><img src="https://img.shields.io/badge/LinkedIn-Nicholas%20Tweedie-0A66C2?style=flat-square" alt="LinkedIn"></a>
  <a href="mailto:ntweedie@uci.edu"><img src="https://img.shields.io/badge/Email-ntweedie@uci.edu-333333?style=flat-square&logo=gmail&logoColor=white" alt="Email"></a>
  <a href="https://huggingface.co/nicholashat"><img src="https://img.shields.io/badge/Hugging%20Face-nicholashat-FFD21E?style=flat-square&logo=huggingface&logoColor=black" alt="Hugging Face"></a>
</p>

> [!NOTE]
> **Looking for a Summer 2027 software engineering internship.** B.S. Software Engineering, UC Irvine, June 2028 · GPA 3.6

I like building software that solves real problems. Most of my recent work is running LLMs on-device, building local-first AI tools, and turning research papers into data a lab can actually use.

## Experience

**Undergraduate Research Assistant, Software** · Zenyuk Lab, National Fuel Cell Research Center, UCI · *Apr 2026 – present*
<br>Built [rare-earth-extraction](https://github.com/NicholasHat/rare-earth-extraction), an AI tool that pulls data out of charts in chemistry papers.
- Extracted 4,800+ data points from 50+ open-access papers at about $0.37 per paper (Claude Batches API)
- Caught points the model silently dropped by reading marker positions straight from each PDF's vector geometry
- Crash-safe batch runner that can stop and resume without paying twice, plus a human review queue and 460+ tests

`Python` `Claude API` `pdfplumber` `Streamlit` `SQLite`

## Projects

### [ZeroHop](https://github.com/NicholasHat/ZeroHop)
Made LLM text generation faster on a Mac by splitting the work across the Neural Engine and the GPU.
- **1.47x faster** decoding on an M3 (28.1 vs 19.1 tokens/sec) with identical output, using a 1B draft model and an 8B target
- Cut the chip-to-chip handoff delay from 1.33 ms to 165 µs after my measuring tool found power-state behavior missing from Apple's docs

`Swift` `Python` `Core ML` `MLX` `Metal`

### [oss-instruct-py](https://github.com/NicholasHat/oss-instruct-py)
Fine-tuned a code-writing LLM on synthetic training data I generated.
- Raised HumanEval pass@1 from **67.7% to 70.7%** by LoRA fine-tuning Qwen2.5-Coder-3B on ~28K examples ([adapter on Hugging Face](https://huggingface.co/nicholashat/qwen2.5-coder-3b-oss-instruct-lora))
- Traced a repeatable 7B training crash to MLX memory corruption and fixed it, halving peak memory to 6.6 GB

`Python` `MLX` `Hugging Face` `LoRA`

### [rate-limiter](https://github.com/NicholasHat/rate-limiter)
Three API rate limiters on AWS, load-tested side by side.
- Load tests found a race condition letting **35 requests through a limit of 10**; an atomic DynamoDB write brought it to 11
- Measured the cost of correctness: p99 response time went from 163 ms to about 380 ms

`Python` `AWS Lambda` `DynamoDB` `Terraform` `k6`

### [project-steward](https://github.com/NicholasHat/project-steward)
Rebuilds a project's timeline, gaps, and drift from a messy folder of files, with every claim linked to its source.
- 11-stage pipeline that reads PDFs, Word, PowerPoint, spreadsheets, images, and text
- Deploys with one `docker compose up`; CI runs 210+ tests against a live Postgres database on every push

`Python` `FastAPI` `PostgreSQL` `pgvector` `React` `Docker`

### [local-AI](https://github.com/NicholasHat/local-AI)
A private ChatGPT-style assistant that runs entirely on your own machine.
- Tool calling, document search (RAG), PDF form filling, and a coding agent that can't change anything until a human approves the diff
- 345 tests run without a live model

`Python` `FastAPI` `React` `TypeScript` `Ollama`

### [Pointer](https://github.com/har-m33t/claude-socal-affordable-housing-hackathon) · Claude Impact Lab hackathon, team of 5
Walks homeowners through their city's backyard-home (ADU) permit paperwork, answering only from the city's own documents.
- Wrote in-browser redaction that strips names, addresses, and parcel numbers before anything reaches Claude

`TypeScript` `Next.js` `React` `Claude API`

## Skills

| | |
| :--- | :--- |
| **Languages** | Python, TypeScript, JavaScript, Swift, C++, SQL, Java |
| **AI / ML** | LoRA fine-tuning, Core ML, MLX, Hugging Face, Claude API, Ollama, RAG, tool calling |
| **Backend and cloud** | FastAPI, PostgreSQL/pgvector, SQLite, AWS (Lambda, API Gateway, DynamoDB, S3), Docker, Terraform, GitHub Actions |
| **Frontend** | React, Next.js, TailwindCSS, Streamlit |
