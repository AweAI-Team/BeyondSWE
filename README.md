# BeyondSWE: Can Current Code Agent Survive Beyond Single-Repo Bug Fixing?

<div align="center">

[![Hugging Face Datasets](https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Datasets-blue)](https://huggingface.co/datasets/Awe-AI/BeyondSWE)
[![Hugging Face Models](https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Models-yellow)](https://huggingface.co/Awe-AI/BeyondSWE)
[![License](https://img.shields.io/badge/License-CC%20BY%204.0-green.svg)](LICENSE)
[![Website](https://img.shields.io/badge/%F0%9F%8C%90_Project-Website-blue.svg)](https://aweai-team.github.io/BeyondSWE/)
<br>

</div>

![](figures/beyondswe.png)

## Abstract

Current benchmarks for code agents primarily assess narrow, repository‑specific fixes, overlooking critical real‑world challenges such as cross‑repository reasoning, domain‑specialized problem solving, dependency‑driven migration, and full‑repository generation. To address this gap, we introduce BeyondSWE, a comprehensive benchmark that broadens existing evaluations along two axes—resolution scope and knowledge scope—using 500 real‑world instances across four distinct settings. Experimental results reveal a significant capability gap: even frontier models plateau below 45% success, and no single model performs consistently across task types. To systematically investigate the role of external knowledge, we develop SearchSWE, a framework that integrates deep search with coding abilities. Our experiments show that search augmentation yields inconsistent gains and can in some cases degrade performance, highlighting the difficulty of emulating developer‑like workflows that interleave search and reasoning during coding tasks. This work offers both a realistic, challenging evaluation benchmark and a flexible framework to advance research toward more capable code agents.

## Benchmark Tasks

- **🔗 CROSS-REPOSITORY**: Requires consulting related projects, upstream libraries, and external dependencies—beyond a single codebase, containing 200 tasks.
- **🧬 DOMAIN-SPECIFIC**: Demands specialized scientific expertise (e.g., chemistry, quantum computing) in addition to programming skills, containing 72 tasks.
- **🕊️ DEPENDENCY-DRIVEN MIGRATION**: Moves from localized patches to codebase-wide transformations triggered by dependency upgrades (e.g., Pydantic v1→v2), containing 178 tasks.
- **📝 DOCUMENT-TO-REPOSITORY**: Builds an entire functional repository from specifications such as design docs or API descriptions, containing 50 tasks.

## Results & Analysis

We evaluate frontier models with our scaffold: **SearchSWE**, and compare against the OpenHands baseline. Results highlight a key gap: search and coding abilities have improved independently, but their integration remains inconsistent in practice.

![](figures/beyondswe_performance.png)

We conducted a detailed analysis of the experimental results in our paper.

## License

This project is licensed under the CC BY 4.0 License - see the [LICENSE](LICENSE) file for details.
