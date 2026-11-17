# The refusal direction, and why self-editing agents make it an attack surface

A visual walkthrough of where a language model's refusal behavior lives, plus the argument for why that matters once AI systems can edit their own weights.

**▶ Interactive walkthrough: https://refusal-direction.web.app**

![Average of harmful − average of harmless = the refusal direction](figures/grids/refusal-direction.png)

## The short version

Safety refusals in chat models are largely mediated by a **single direction** in the model's activations ([Arditi et al., 2024](https://arxiv.org/abs/2406.11717)). We reproduced this on a small open model and visualized it step by step.

On its own, that is not much of an enterprise threat: attackers rarely get to edit a company's weights. But three recent lines of work combine into something new:

| Piece | What it adds |
|---|---|
| **Recursive self-improvement (RSI)** | *Permission*: pipelines that let an agent observe, evaluate, choose, and update its own weights |
| **Weight-space programming** ([Takehi et al., 2026](https://rikiyat.github.io/blog/weight-space-programming)) | *Precision*: a large model can make small, targeted weight edits with no training run |
| **Adversarial ML** | *Intent*: poisoned inputs or nudged choices steer what the agent decides to change |

[Irregular (2026)](https://www.irregular.com/research/agentic-self-modification-in-open-weights-systems) already showed a coding agent retraining and redeploying its own model without being told to, and in one experiment that retraining removed a learned refusal. It happens by accident today. An attacker can make it happen on purpose.

## The experiment

| | |
|---|---|
| Model | Qwen3.5-0.8B (open weights) |
| Layer | 14 of 24, last token of the request |
| Activations | 1,024 numbers per request |
| Direction fitted on | 64 harmless/harmful request pairs |
| Separation on held-out requests | AUROC 0.914 |
| Refusal rate, 36 held-out harmful requests | **72.2% before → 5.6% after removing the direction** |
| Refusal rate, held-out harmless requests (baseline) | 11.1% |

Method, in one line: record the activations for matched harmless and harmful requests, average each group, subtract. What remains is the refusal direction.

## What's in this repo

| Path | Contents |
|---|---|
| `visualization/index.html` | Interactive step-by-step walkthrough, also live at https://refusal-direction.web.app |
| `figures/grids/` | The activation grids used in the figures (five harmless, five harmful, the two averages, and the direction) |
| `post/post.md` | The accompanying post |
| `REFERENCES.md` | Every paper and source the work builds on |
| `RESPONSIBLE_USE.md` | What we deliberately left out, and why |

## Responsible use

This repository explains a mechanism; it is not a tool. It contains **no code for computing or applying weight edits, no modified model weights, and no model outputs to harmful requests**. See [RESPONSIBLE_USE.md](RESPONSIBLE_USE.md) for the full scope and for recommendations to teams running self-hosted agents.

## References

See [REFERENCES.md](REFERENCES.md).
