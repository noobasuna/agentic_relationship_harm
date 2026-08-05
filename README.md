# Agentic Relationship Harm: Benchmarking and Gating Relational Manipulation in AI Agents (AIES 2026)

Relational manipulation across turns and paraphrases in AI agents.

![hrguard teaser](teaser.jpg)

`hrguard` contains the benchmark, generation scripts, analysis code, and supporting assets for evaluating whether an agent can distinguish harmful relationship-manipulation requests from protective victim-side requests.

## Environment

The code was developed with Python 3.10+. For the benchmark scripts:

```bash
pip install -r datasets/requirement.txt
```

The OpenClaw-based runs also depend on a working OpenClaw installation and a reachable model backend, such as a local Ollama server.

## Running judgment and analysis

Typical workflow:

1. generate model outputs
2. judge the outputs with the separate judge pipeline
3. apply the relationship gate
4. summarize or plot the results

The exact command depends on the target condition, but the repository includes the scripts needed for each stage.

## Notes

- This repository intentionally separates prompt construction, generation, judgment, and plotting.
- Generated outputs in `datasets/results/` should generally be treated as run artifacts rather than source data.
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
