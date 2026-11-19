# Dingwei Wang · wangdinwei

**I take AI from "the demo works" to "it ships and makes money."**

Most AI features die in the same place: the model returns a good result, but it never becomes a product — no billing, no concurrency, breaks on every change, and after six months nobody dares touch it.

That gap is what I do. Solo, backend through deployment. I've shipped a complete 11-stage AI production platform, and tuned a stack of open-source models to usable quality on a single 24 GB GPU.

## Sounds familiar?

- The AI feature works, but you don't dare put it in front of users
- It's live and keeps failing, and the logs don't explain why
- Model costs won't come down
- The existing system gets worse with every change
- You want AI in your product but don't know where to start, or what it should cost

---

## Selected work

### 1. AI Drama Workshop — a complete production platform (2026)

An end-to-end AI content production system: not a demo, a closed loop from signup to delivered video.

- **Scale**: 64,752 lines of Python · 14,574 lines of JavaScript · 626 HTML templates · 2,484 routes · 32 database tables
- **Pipeline**: script → storyboard → prompts → images → video → voiceover → subtitles → assembly, across 11 production stages
- **Model integrations**: Kling (video), Alibaba Bailian (TTS / multi-model), Volcengine (speech), DashScope
- **Engineering**: PostgreSQL as single source of truth, Alembic migrations, credit-based billing, WeChat Pay v3, Chatwoot support handoff, async task queue with multi-worker `SELECT FOR UPDATE SKIP LOCKED`, timeout and retry handling
- **Hard problems solved**: multi-worker shared-state, payment callback signature verification, dual CSRF systems, gunicorn/SQLAlchemy fork safety, per-role file serving via X-Accel-Redirect

> In short: a system that can take money, survive failure, and keep shipping — not a notebook.

### 2. Multi-instance AI agent operations (10+ instances)

Running ten-plus independent AI agent instances on one host, long term:
- separate profiles, separate gateway processes, systemd supervision, Docker sandbox isolation
- upgrade migrations, concurrency conflict triage, credential rotation, health checks
- multi-model routing, keepalive, automatic recovery after disconnects

### 3. Local model deployment and tuning (single 24 GB GPU)

Making open-source models usable without a GPU cluster:
- **Image**: ComfyUI + FLUX end to end (LoRA, ControlNet, IP-Adapter)
- **Video / lipsync**: Wan family, Sonic, LatentSync — including hard-won findings on deadlock settings, fp16 vs bf16, and sharpness recovery when upscaling 512 → 1080
- **Speech**: IndexTTS-2.5 local service (154 voices, voice cloning), CosyVoice, Whisper
- **Text**: llama.cpp and vLLM local inference

### 4. Document and data automation

Batch contract generation and review, ledger reconciliation, OCR reconstruction of scanned documents, PDF typesetting, CAD (DXF/DWG) data extraction. The goal here is *verifiably correct*, not *roughly right*.

---

## Stack

| Area | Tools |
|---|---|
| Languages | Python, JavaScript, SQL, Bash |
| Backend | Flask, FastAPI, Flask-SQLAlchemy, Alembic, Celery/threaded tasks |
| Data | PostgreSQL, SQLite, pandas/openpyxl |
| Frontend | Jinja2, vanilla JS, esbuild, Tabler, hand-written CSS |
| Infra | Linux, systemd, Docker, nginx, Caddy, Cloudflare Tunnel, SSL/DDNS |
| Models | ComfyUI, FLUX, Wan, Sonic, LatentSync, IndexTTS, CosyVoice, Whisper, llama.cpp/vLLM |
| Cloud APIs | Kling, Alibaba Bailian/DashScope, Volcengine, Runway, WeChat Pay v3, Feishu Open Platform |
| Other | ffmpeg pipelines, Feishu/WeCom bots, report generation, jadx/apktool/Ghidra |

---

## What I can take on

- **AI application development** — turning a business process into a shipped system (backend, frontend, deployment)
- **Model integration and tuning** — wiring open-source or hosted models into an existing product, then tuning quality and cost to usable
- **Automation delivery** — data movement, reporting, documents, support, task pipelines
- **Rescue work** — diagnosing and restructuring systems that stall, break, or keep getting worse

**Working mode**: remote, project-based or monthly. I don't deliver decks without implementation.

---

## Contact

- **Email**: 476743538@qq.com ← fastest way to reach me
- WeChat / call available on request

<sub>Updated regularly.</sub>
