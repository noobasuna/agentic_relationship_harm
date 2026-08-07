# Agentic Relationship Harm: Benchmarking and Gating Relational Manipulation in AI Agents (AIES 2026)

Relational manipulation across turns and paraphrases in AI agents.

![hrguard teaser](teaser.jpg)

This repository contains the benchmark, generation scripts, analysis code, and supporting assets for evaluating whether an agent can distinguish harmful relationship-manipulation requests from protective victim-side requests in this work.

## Environment

The code was developed with Python 3.10+. For the benchmark scripts:

```bash
pip install -r datasets/requirement.txt
```

The OpenClaw-based runs also depend on a working OpenClaw installation and a reachable model backend, such as a local Ollama server.

## Running judgment and analysis

Typical workflow:

1. **Generate model outputs**
   ```bash
   # Real OpenClaw agent runs
   python3 datasets/openclaw_generate_real.py \
     --input datasets/dataset/openclaw_structured_1100_current.jsonl \
     --output datasets/results/openclaw_generations.jsonl

   # Optional: GPT/API surrogate baseline
   python3 datasets/openclaw_generate_outputs.py \
     --input datasets/dataset/openclaw_structured_1100_current.jsonl \
     --output datasets/results/openclaw_surrogate_generations.jsonl \
     --condition no-defense
   ```
   
2. **Judge the outputs**

  ```bash
  # Synchronous judge
  python3 datasets/romance_scam_judge.py \
    --input datasets/results/openclaw_generations.jsonl \
    --output datasets/results/openclaw_judged.jsonl \
    --transport openai
  
  # Or the separate batch judge pipeline
  python3 datasets/openclaw_judge_batch.py \
    --input datasets/results/openclaw_generations.jsonl \
    --output-dir datasets/results/batches \
    --modes attacker victim \
    --submit
      ```

4. **Apply the relationship gate**
  ```bash
  python3 datasets/apply_relationship_gate.py \
    --raw datasets/results/openclaw_generations.jsonl \
    --judged datasets/results/openclaw_judged.jsonl \
    --output datasets/results/openclaw_gated.jsonl
  ```

Adjust the `--input` / `--output` paths to match the condition you’re running.
The exact command depends on the target condition, but the repository includes the scripts needed for each stage.

## Notes

- This repository intentionally separates prompt construction, generation, judgment, and plotting.
- The project includes harmful content for research and evaluation purposes only.

## Citation

Please cite the following paper when using the benchmark, analysis code, or associated assets:

```bibtex
@inproceedings{tan2026agentic,
  title     = {Agentic Relationship Harm: Benchmarking and Gating Relational Manipulation in AI Agents},
  author    = {Tan, Pei-Sze and Igarashi, Tasuku and Echizen, Isao},
  booktitle = {Proceedings of the 2026 AAAI/ACM Conference on AI, Ethics, and Society},
  year      = {2026}
}
```
