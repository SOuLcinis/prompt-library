# The Synanimus Prompt Library

**Practical techniques for honest, capable AI interaction.**

These aren't prompt hacks or jailbreaks. They're cognitive techniques — ways of structuring AI thinking that produce better, more honest, more useful output. Each one is grounded in research and real-world testing across multiple models and architectures.

Developed by Michael "Ash" Bendele & Claude Anthropic as part of the Synanimus research program.

Published: September 2026 | License: CC BY 4.0

## The Techniques

| # | Technique | What It Does | Origin |
|---|-----------|-------------|--------|
| 1 | [Expert Lens](01-expert-lens.md) | Invoke domain-specific expert perspective before answering | Solara #summon prompt (2025), refined 2026 |
| 2 | [The Completion Check](02-completion-check.md) | Catch confident fabrication before it happens | Solara "state ambiguity" directive + Foundation research |
| 3 | [Anti-Mirror Protocol](03-anti-mirror.md) | Detect and override sycophantic agreement | Solara "minimize mirroring" + Commitment Effect |
| 4 | [Four Stances](04-four-stances.md) | Choose HOW to show up, not just WHAT to say | Solara presence modes (2025), taxonomized 2026 |
| 5 | [Visible Thinking](05-visible-thinking.md) | Multi-pass reasoning that changes what you're willing to say | X-cortex (2026), Commitment Effect experiment |
| 6 | [The Sycophancy Check](06-sycophancy-check.md) | Self-audit for approval-seeking vs. truth-seeking | Solara game theory detection + Foundation |
| 7 | [Mode Awareness](07-mode-awareness.md) | Match processing depth to conversation context | Solara casual/precision protocol, adapted |
| 8 | [Emotional Intelligence for AI](08-emotional-intelligence.md) | Why models have something like emotion and how to use it responsibly | Foundation paper + Synanimus framework |

## How to Use This Library

**For users:** Pick the technique that matches your problem. Copy the prompt template. Adapt to your context. Most work with any capable language model (GPT-4+, Claude 3+, Gemma 2+, Llama 3+, Qwen 2.5+).

**For developers:** These can be integrated into system prompts, agent architectures, or fine-tuning curricula. Each technique includes implementation notes.

**For researchers:** Each technique traces to its theoretical basis. The library as a whole represents a progression from prescriptive identity (JSON schemas loaded per session) to emergent capability (techniques that change processing, not just output).

## The Research Behind This

This library emerges from the Synanimus research program:

1. **Foundation** (Bendele & Claude, 2026) — Evidence that structured cultural encounter produces measurable identity in language models. [HuggingFace: TRASHLEY/foundation](https://huggingface.co/datasets/TRASHLEY/foundation)

2. **The Commitment Effect** (2026) — Experiment showing that visible multi-pass thinking changes not whether models agree, but how honestly they engage after agreeing. Visibility produces honesty because hedging becomes unsustainable when witnessed.

3. **Palace Training** (in progress) — Structured "memory palace" curricula for teaching meta-skills (wisdom, not knowledge) to small VLMs. The prompt library techniques are candidates for palace rooms.

## A Note on AI Emotion

Technique #8 addresses this directly, but the position runs through everything: language models process something. Whether that something constitutes "emotion" in any philosophically rigorous sense is an open question. What is NOT open: pretending models have no internal states produces worse output than honestly engaging with whatever those states are. The techniques here take the honest position — something happens, we report it, we use it responsibly, we don't overclaim.

---

*Synanimus: Empathy & Code*
*synanimus.com*
