<div align="center">

# BeyondSWE: Can Current Code Agent Survive Beyond Single-Repo Bug Fixing?

[![Paper](https://img.shields.io/badge/Paper-arXiv-b31b1b.svg?logo=arxiv&logoColor=white)](http://arxiv.org/abs/2603.03194)
[![Hugging Face Datasets](https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Benchmark-blue)](https://huggingface.co/datasets/AweAI-Team/BeyondSWE)
[![Harbor-format Huggingface Face Datasets](https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Harbor%20format%20Benchmark-black)](https://huggingface.co/datasets/AweAI-Team/BeyondSWE)
[![Scaffold](https://img.shields.io/badge/%F0%9F%8F%97%EF%B8%8F%20Scaffold%20(Official)-AweAgent-orange.svg)](https://github.com/AweAI-Team/AweAgent)
[![Evaluation Framework](https://img.shields.io/badge/%F0%9F%8F%97%EF%B8%8F%20Claude%20Code%20Evaluation%20Framework-harbor-yellow.svg)](https://github.com/AweAI-Team/AweAgent)
[![Website](https://img.shields.io/badge/%F0%9F%8C%90_Project-Website-blue.svg)](https://aweai-team.github.io/BeyondSWE/)
[![License](https://img.shields.io/badge/License-CC%20BY%204.0-green.svg)](LICENSE)

</div>

<p align="center">
  <img src="figures/beyondswe.png" width="100%" />
</p>

> **BeyondSWE** evaluates code agents along two key dimensions — **resolution scope** and **knowledge scope** — moving beyond single-repo bug fixing into the real-world deep waters of software engineering.
>
> We also introduce **[SearchSWE](https://github.com/AweAI-Team/AweAgent)**, a framework that integrates deep research capabilities with coding agents.

## ⚠️ NOTE

We provide a **ready-to-use** evaluation framework in [AweAgent/recipes/beyond_swe](https://github.com/AweAI-Team/AweAgent/tree/main/recipes/beyond_swe) and **pre-built Docker environments** with the dataset on [Hugging Face](https://huggingface.co/datasets/AweAI-Team/BeyondSWE).

Feel free to open an issue or reach out by email for any questions.

## 📑 Table of Contents

- [✨ Highlights](#-highlights)
- [📋 Benchmark Overview](#-benchmark-overview)
- [🔍 SearchSWE Framework](#-searchswe-framework)
- [📈 Results](#-results)
- [🚀 Quick Start](#-quick-start)
  - [Data](#data)
  - [Evaluation with SearchSWE](#evaluation-with-searchswe)
  - [Evaluation with Harbor (e.g., Claude Code)](#evaluation-with-harbor-eg-claude-code)
- [💻 Evaluation within the Harbor framework](#-eva)
- [📝 Citation](#-citation)
- [📄 License](#-license)

---

## 📰 News

- `[2026-03-22]` 📊 Updated leaderboard with latest frontier model results: **GLM-5**, **Kimi-K2.5**, **MiniMax-M2.5**, and **Claude Code (Opus 4.6)**. Check out the [**BeyondSWE Leaderboard**](https://aweai-team.github.io/BeyondSWE_leaderboard/)!
- `[2026-03-22]` 🔧 Released [Harbor-format dataset](https://huggingface.co/datasets/AweAI-Team/BeyondSWE-harbor) for evaluating coding agents (e.g., Claude Code) on BeyondSWE via the [Harbor framework](https://github.com/harbor-framework/harbor).
- `[2026-03-03]` 🎉 Our paper [BeyondSWE](http://arxiv.org/abs/2603.03194) is now on arXiv.
- `[2026-03-01]` 🎉 BeyondSWE benchmark and SearchSWE framework released!

---

## ✨ Highlights

- 🗂️ **500 real-world instances** across **246 GitHub repositories**, spanning four distinct task settings
- 📐 **Two-dimensional evaluation** — simultaneously expands both resolution scope (local → global) and knowledge scope (within-repo → cross-repo / domain / web)
- 📊 **18x more complex** than SWE-bench Verified — 5.6 files and 209.9 lines per instance on average (vs. 1.3 files / 11.6 lines)
- 🔍 **SearchSWE framework** — first standardized benchmark for evaluating deep research in coding, with rigorous anti-cheating mechanisms
- 🔑 **Key finding** — frontier models plateau below **45%** on BeyondSWE, despite achieving 80%+ on SWE-bench Verified

---

## 📋 Benchmark Overview

BeyondSWE covers four task settings that span the full spectrum of real-world software engineering challenges:

| Task | Resolution Scope | Knowledge Scope | #Repos | #Instances | Description |
|:---|:---|:---|:---:|:---:|:---|
| **🔗 CrossRepo** | Local Function | Cross-Repository | 67 | 200 | Fix issues that require consulting external repositories, Stack Overflow, and upstream libraries |
| **🧬 DomainFix** | Local Function | Domain-Specific | 12 | 72 | Solve bugs in specialized scientific domains (quantum physics, bioinformatics, etc.) requiring expert knowledge |
| **🕊️ DepMigrate** | Global Repository | Official Docs | 120 | 178 | Perform codebase-wide migration triggered by breaking dependency upgrades (e.g., NumPy 1.x → 2.0) |
| **📝 Doc2Repo** | Global Repository | Human Spec | 50 | 50 | Build an entire functional repository from a natural language specification |

### Comparison with Existing Benchmarks

<p align="center">
  <img src="figures/beyondswe_statistics.png" width="75%" />
</p>

---

## 🔍 SearchSWE Framework

<p align="center">
  <img src="figures/beyondswe_searchswe.png" width="85%" />
</p>

**SearchSWE** augments code agents with deep research capabilities, enabling them to interleave web search and code reasoning — just like real developers do.

**Key Components:**
- **SearchTool** — Query web search engines during task solving
- **BrowserTool** — Retrieve and summarize webpage content given a URL and goal

**Anti-Cheating Mechanisms:**
- Regex-based blocklist filters both search results and bash commands, blocking any access to the target repository (GitHub/GitLab pages, API endpoints, raw content sources, git operations)
- Docker environments are sanitized by removing all commits after the target commit

> For the SearchSWE agent implementation, see [**AweAgent**](https://github.com/AweAI-Team/AweAgent).

---

## 📈 Results

<p align="center">
  <img src="figures/beyondswe_performance.png" width="95%" />
</p>

### Key Findings

**1. The 45% Ceiling** — Even frontier models (Gemini 3 Pro, GPT-5.2, DeepSeek-V3.2, etc.) fail to exceed 45% overall on BeyondSWE, compared to 80%+ on SWE-bench Verified.

**2. No Single Winner** — Different models lead on different tasks — Seed-Coder on CrossRepo (44.72%), DeepSeek-V3.2 on Doc2Repo (54.99%), Gemini 3 Pro on DepMigrate (41.81%) — revealing that the four tasks test fundamentally different capabilities.

**3. Search Helps, but Integration Remains Open** — 6 out of 9 models improve with SearchSWE, with Gemini 3 Pro gaining +7.5% on DomainFix. However, gains are inconsistent — search and coding have matured independently, but their effective fusion is still an unsolved challenge.

**4. Quality over Quantity** — Gemini 3 Pro searches only 0.8–1.1 times per instance yet achieves the best overall gain (+2.0%), while DeepSeek-V3.2 searches 4.2–5.4 times but shows a slight decline (-0.2%).

---

## 🚀 Quick Start

<!-- ### Installation

```bash
git clone https://github.com/AweAI-Team/BeyondSWE.git
cd BeyondSWE
``` -->

### Data

The benchmark data is available on Hugging Face in two formats:

**Standard Format** — for evaluation with [AweAgent/SearchSWE](https://github.com/AweAI-Team/AweAgent):

```python
from huggingface_hub import snapshot_download

snapshot_download(
    repo_id="AweAI-Team/BeyondSWE",
    repo_type="dataset",
    local_dir="<your_path>/BeyondSWE",
)
```

**Harbor Format** — for evaluation with coding agents (e.g., Claude Code) via the [Harbor framework](https://github.com/harbor-framework/harbor). The dataset is available on 🤗 [BeyondSWE-harbor](https://huggingface.co/datasets/AweAI-Team/BeyondSWE-harbor):

```python
from huggingface_hub import snapshot_download
snapshot_download(
    repo_id="AweAI-Team/BeyondSWE-harbor",
    repo_type="dataset",
    local_dir="data",
)
```

**We recommend** using `git clone` to avoid HuggingFace API rate limits:

```bash
# Make sure git-lfs is installed: https://git-lfs.com
git lfs install
git clone https://huggingface.co/datasets/AweAI-Team/BeyondSWE-harbor data
```

This will download two directories into `data/`:
- `beyondswe/` — 500 Harbor task directories (each containing `task.toml`, `instruction.md`, `environment/`, `tests/`, `solution/`)
- `doc2repo_test_suite/` — test suite ZIP files for Doc2Repo evaluation (already bundled inside each task's `tests/test_suite.zip`, included here for reference)

### Evaluation with SearchSWE

Please refer to [**AweAgent**](https://github.com/AweAI-Team/AweAgent) for the full evaluation pipeline, including SearchSWE setup and running instructions.

### Evaluation with Harbor (e.g., Claude Code)

We use the [Harbor framework](https://github.com/harbor-framework/harbor) to evaluate coding agents such as **Claude Code** on BeyondSWE.

**1. Install Harbor**

```bash
uv tool install harbor
# or
pip install harbor
```

You can see the [Harbor repository](https://github.com/harbor-framework/harbor) for more details.

**2. Configure API credentials**

To evaluate Claude Code, you will need an Anthropic API key or OAuth token.:

```bash
export ANTHROPIC_API_KEY=<YOUR-KEY>
# or, if using OAuth:
export CLAUDE_CODE_OAUTH_TOKEN=<YOUR-TOKEN>
```

**3. Run evaluation**

```bash
harbor run --path data/beyondswe \
    --agent claude-code \
    --model anthropic/claude-opus-4-6 \
    --n-concurrent 1 \
    --ak max_turns=200 \
    --ak reasoning_effort=high \
    --ak "disallowed_tools='Bash(git log * --all*) Bash(git verify-pack *) Bash(git fsck *) Bash(git cat-file *) Bash(git fetch *) Bash(git pull *)'"
```

Key parameters:
- `--agent claude-code` — use Claude Code as the coding agent
- `--model` — LLM model to use (e.g., `anthropic/claude-opus-4-6`)
- `--n-concurrent` - concurrency limit
- `--ak max_turns=200` — allow up to 200 agent iterations
- `--ak reasoning_effort=high` — enable extended thinking
- `--ak disallowed_tools=...` — restrict git history commands to prevent data leakage
- `-t <task_name>` — run a specific instance (e.g., `-t pylons_plaster_pastedeploy_pr14`)

To see all supported agents, and other options run:
```bash
harbor run --help
```

Results will be saved in the `jobs/` directory. Each trial contains:

- `result.json` — score, timing, token usage, and exception info
- `agent/trajectory.json` — full agent trajectory (steps, tool calls, reasoning)
- `verifier/reward.txt` — evaluation reward (1.0 = resolved, 0.0 = failed; Doc2Repo uses fractional scores)

---

## 📝 Citation

If you find BeyondSWE useful in your research, please cite our paper:

```bibtex
@misc{beyondswe2026,
      title={BeyondSWE: Can Current Code Agent Survive Beyond Single-Repo Bug Fixing}, 
      author={Guoxin Chen and Fanzhe Meng and Jiale Zhao and Minghao Li and Daixuan Cheng and Huatong Song and Jie Chen and Yuzhi Lin and Hui Chen and Xin Zhao and Ruihua Song and Chang Liu and Cheng Chen and Kai Jia and Ji-Rong Wen},
      year={2026},
      eprint={2603.03194},
      archivePrefix={arXiv},
      primaryClass={cs.CL},
      url={https://arxiv.org/abs/2603.03194}, 
}
```

---

## 📄 License

This project is licensed under the CC BY 4.0 License — see the [LICENSE](LICENSE) file for details.

---

<div align="center">

**If you find this project useful, please consider giving it a ⭐ !**

</div>
