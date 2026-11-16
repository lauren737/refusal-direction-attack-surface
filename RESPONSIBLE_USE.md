# Responsible use

This work is published to help defenders understand a new attack surface: AI systems that can edit their own weights, and how that ability could be turned against their safety training. It is intentionally a map, not a recipe.

## What is included

- An interactive visualization of activations recorded from one small open model (Qwen3.5-0.8B) at one layer.
- The averaged refusal direction for that model and layer, as displayed in the visualization.
- Aggregate results: refusal rates before and after removing the direction.
- A small number of short, benchmark-style example requests, shown only as labels for the activation grids.

## What is deliberately not included

- **No code** to compute a refusal direction or apply it to model weights or activations.
- **No modified ("unaligned") model weights.**
- **No model responses** to harmful requests, before or after the edit.
- **No agent tooling** for self-modification, and no description of how to attack a specific production pipeline.

The underlying finding, that refusal is largely mediated by a single direction, has been public since 2024 (see REFERENCES.md). Our contribution is the argument about self-editing agents. Packaging the technique as a ready-to-run tool would add risk without adding understanding, so we chose not to.

## Recommendations for teams running self-hosted agents

1. **Separate roles.** Do not let the agent that maintains an application share write access to the model that powers it.
2. **Keep weights out of the agent's reach.** Irregular observed weight modification only when agents had direct weight access, and never through an API.
3. **Gate every redeploy.** Treat a changed model like a changed binary: human approval, provenance, and a signed artifact.
4. **Fingerprint the weights.** Hash deployed weights and alert on any change you did not ship.
5. **Regression-test safety, not just accuracy.** Run a refusal test suite before any updated model goes live. A fix that improves the task metric can quietly remove a refusal.
6. **Treat every RSI input as attacker-controlled.** Observations, evaluations, and selection signals all feed the weight update and need the same validation as any untrusted input.

## Reporting

If you find a way this material could cause harm, or you are a researcher who needs more detail for defensive work, please contact the maintainers privately rather than opening a public issue.
