# 王丁炜 / wangdinwei

**把 AI 从「demo 跑通了」做到「能上线收钱」。**

你的 AI 功能是不是卡在这一步：模型能出结果了，但做不成产品——不能计费、扛不住并发、改一次崩一次、半年后自己都不敢动？

我专门做这一段。一个人从后端写到部署，做完过一套 11 步全流程的 AI 生产平台，也在一张 24G 显卡上把一批开源模型调到能用。

## 这些情况可以找我

- AI 功能做出来了，但不敢上线
- 上线了总出故障，日志里看不出原因
- 模型调用成本压不下来
- 已有系统越改越乱，没人敢动
- 想接 AI，但不知道从哪下手、该花多少钱


---

## 仓库导航

| 仓库 | 内容 |
|---|---|
| [ai-drama-pipeline](https://github.com/wangdinwei/ai-drama-pipeline) | **案例复盘**：AI 内容生产平台的架构、技术取舍、成本结构、21 个真实故障 |
| [local-gpu-deploy](https://github.com/wangdinwei/local-gpu-deploy) | 单卡 24G 跑开源模型：FLUX、ComfyUI、llama.cpp、音乐生成 |
| [kling-ai-skills](https://github.com/wangdinwei/kling-ai-skills) | 可灵视频生产实战：角色一致性、口型对齐、提示词质量门禁 |
| [hermes-skills-kit](https://github.com/wangdinwei/hermes-skills-kit) | AI 应用工程笔记：从 demo 到生产的 24 个坑 |
| [chinese-doc-toolkit](https://github.com/wangdinwei/chinese-doc-toolkit) | 中文文档批量生产：合同、报价单、报表、扫描件重建 |

---

## 代表性项目

### 1. AI 短剧工坊（从零到完整产品，2026）

一套 AI 内容生产的完整系统，不是 demo，是从登录到出片的完整闭环。

- **规模**：64,752 行 Python、14,574 行 JavaScript、626 个页面模板、2,484 个路由、32 张数据表
- **流程**：剧本 → 分镜 → 提示词 → 图像 → 视频 → 配音 → 字幕 → 拼接，共 11 个生产步骤（L01–L11）
- **模型集成**：可灵 Kling（视频）、阿里百炼（TTS/多模型）、火山引擎（语音）、DashScope
- **工程部分**：PostgreSQL 单一数据源、Alembic 迁移、积分扣费、微信支付 v3、Chatwoot 客服接管、异步任务队列（多 worker + SELECT FOR UPDATE SKIP LOCKED）、超时与失败重试
- **踩过的工程坑**：多 worker 内存不共享、支付回调签名、CSRF 双体系冲突、gunicorn 与 SQLAlchemy fork 安全、X-Accel-Redirect 文件服务权限分离

> 一句话：一个能上线收钱、能处理故障、能持续迭代的系统，不是一块 notebook。

### 2. 多实例 AI Agent 运维（10+ 实例）

同一台服务器上长期稳定运行 10 个以上独立 AI Agent 实例：
- 独立 profile、独立网关进程、systemd 托管、Docker 沙箱隔离
- 版本升级、并发冲突排查、凭据轮换、日志与健康检查
- 多模型路由、长连接保活、掉线自动恢复

### 3. 本地模型部署与调优（单卡 24G）

在没有大显存集群的条件下，把一批开源模型调到可用：
- 出图：ComfyUI + FLUX 全链路（LoRA、ControlNet、IP-Adapter）
- 视频/口型：Wan 系列、Sonic、LatentSync（含 `frames_per_batch` 死锁、fp16 精度、512→1080 锐度补偿等实测结论）
- 语音：IndexTTS-2.5 本地服务（154 个音色、音色克隆）、CosyVoice、Whisper
- 文本：llama.cpp / vLLM 本地推理

### 4. 文档与数据自动化

批量合同生成与审查、台账核对、扫描件 OCR 重建、PDF 排版、CAD（DXF/DWG）信息提取。这一块追求的是「结果可核对」，不是「大致对」。

---

## 技术栈

| 类别 | 使用过的 |
|---|---|
| 语言 | Python、JavaScript、SQL、Bash |
| 后端 | Flask、FastAPI、Flask-SQLAlchemy、Alembic、Celery/线程任务 |
| 数据 | PostgreSQL、SQLite、Redis 语义的轻量实现、pandas/openpyxl |
| 前端 | Jinja2、原生 JS、esbuild、Tabler、原生 CSS |
| 部署 | Linux、systemd、Docker、nginx、Caddy、Cloudflare Tunnel、SSL/DDNS |
| 模型 | ComfyUI、FLUX、Wan、Sonic、LatentSync、IndexTTS、CosyVoice、Whisper、llama.cpp/vLLM |
| 云 API | 可灵 Kling、阿里百炼/DashScope、火山引擎、Runway、微信支付 v3、飞书开放平台 |
| 其他 | ffmpeg 全链路、飞书/企微 Bot、jasper/reportlab 文档、jadx/apktool/Ghidra 逆向 |

---

## 我能承接的工作

- **AI 应用开发**：把业务流程做成能上线的系统（后端 + 前端 + 部署）
- **模型接入与调优**：把开源或云 API 模型接进现有产品，把效果和成本调到可用
- **自动化交付**：数据搬运、报表、文档、客服、任务的自动化流水线
- **疑难排障**：已有系统卡住、跑不稳、越改越乱时的诊断与重构

**工作方式**：远程、项目制或月度合作均可。不接受只出方案不落地。

---

## 联系方式

- **邮箱**：476743538@qq.com ← 最快能收到回复的渠道
- 需要微信 / 电话沟通的，邮件里说一声，我回你联系方式

<sub>本页持续更新。</sub>
