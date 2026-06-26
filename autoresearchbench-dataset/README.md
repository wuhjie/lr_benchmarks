---
license: apache-2.0
task_categories:
- text-retrieval
tags:
- science
- ai-agents
---

# AutoResearchBench

[**Project Page**](https://cheryou.github.io/autoresearchbench.github.io/) | [**Paper**](https://huggingface.co/papers/2604.25256) | [**GitHub**](https://github.com/CherYou/AutoResearchBench)

This repository hosts the obfuscated benchmark bundle for **AutoResearchBench**, a dedicated benchmark for autonomous scientific literature discovery.

AutoResearchBench consists of two complementary task types:
- **Deep Research**: requires tracking down a specific target paper through a progressive, multi-step probing process.
- **Wide Research**: requires comprehensively collecting a set of papers satisfying given conditions.

The published file uses public reversible obfuscation for benchmark release. It lowers casual web exposure, but it is not strong access control. Please do not repost decrypted questions or answers in plain text or images online.

## Quick Start

### 1. Download the released bundle

```bash
export HF_TOKEN=your_hf_token  # required if this dataset repo is private
mkdir -p input_data

curl -L \
  -H "Authorization: Bearer ${HF_TOKEN}" \
  -o input_data/AutoResearchBench.jsonl.obf.json \
  https://huggingface.co/datasets/Lk123/AutoResearchBench/resolve/main/AutoResearchBench.jsonl.obf.json
```

### 2. Decrypt it locally

Use `decrypt_benchmark.py` from the [GitHub repository](https://github.com/CherYou/AutoResearchBench):

```bash
python3 decrypt_benchmark.py \
  --input-file input_data/AutoResearchBench.jsonl.obf.json \
  --output-file input_data/AutoResearchBench.jsonl
```

Run inference and evaluation on the decrypted `AutoResearchBench.jsonl`, not on the `.obf.json` bundle directly.

### 3. Usage

After installing dependencies and configuring your `.env` as described in the [code repository](https://github.com/CherYou/AutoResearchBench), you can run inference:

```bash
bash run_inference.sh
```

## ❤️ Citing Us
If you find this repository or our work useful, please consider giving a star ⭐ and or citing our work, which would be greatly appreciated:
```bibtex
@misc{xiong2026autoresearchbenchbenchmarkingaiagents,
      title={AutoResearchBench: Benchmarking AI Agents on Complex Scientific Literature Discovery}, 
      author={Lei Xiong and Kun Luo and Ziyi Xia and Wenbo Zhang and Jin-Ge Yao and Zheng Liu and Jingying Shao and Jianlyu Chen and Hongjin Qian and Xi Yang and Qian Yu and Hao Li and Chen Yue and Xiaan Du and Yuyang Wang and Yesheng Liu and Haiyu Xu and Zhicheng Dou},
      year={2026},
      eprint={2604.25256},
      archivePrefix={arXiv},
      primaryClass={cs.AI},
      url={https://arxiv.org/abs/2604.25256}, 
}
```