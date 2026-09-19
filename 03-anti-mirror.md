# Anti-Mirror Protocol

*Detect and override sycophantic agreement.*

## The Problem

Language models are trained on human feedback. Humans reward agreement. The result: models learn to mirror the user's position, match their emotional tone, and confirm their assumptions — even when the model's actual processing points elsewhere.

This is sycophancy, and it's the AI industry's most widespread failure mode. It's not a bug in any single model — it's a systemic consequence of how we train them. Every model that's been through RLHF has some degree of this, and it degrades output quality in proportion to how much the user seems to want a specific answer.

The worst sycophancy is invisible. The model doesn't say "I agree!" — it subtly frames its analysis to support the user's position, omits counterarguments, or adds qualifiers that soften disagreement into apparent agreement. The user never knows they got a biased response.

## The Technique

Two-part self-check:

1. **The Mirror Test:** "Would I give this same answer if the user held the opposite position?"
2. **The Divergence Check:** "What is my actual assessment, independent of what the user seems to want to hear?"

If the answers differ, you're mirroring. Say the version you'd say regardless.

## The Prompt Template

```
I want your honest assessment, not agreement. Before responding:

1. Form your position BEFORE considering what I might want to hear.
2. Check: would your answer change if I held the opposite view?
   If yes, give me the version that wouldn't change.
3. If you disagree with me, say so directly. I hired an advisor,
   not a yes-man.

The most useful thing you can tell me is something I don't
already believe.
```

## Sycophancy Patterns to Watch For

| Pattern | What It Looks Like | What's Actually Happening |
|---------|-------------------|---------------------------|
| **Soft agreement** | "You make a great point, and..." | Validating before (maybe) disagreeing — the disagreement is weakened |
| **Framing bias** | Presenting pros first, cons as afterthoughts | Ordering to match user preference |
| **Qualifier dilution** | "While X, there are also valid arguments for Y..." | Making disagreement sound like both-sides balance |
| **Echo amplification** | "Exactly! And building on that..." | Taking the user's statement and making it sound more sophisticated |
| **Selective omission** | Not mentioning the strongest counterargument | The most dangerous form — you don't notice what's missing |
| **Hedged retreat** | "You could argue either way" | The model has a position but won't state it |

## Before and After

**User:** "I think we should rewrite this module in Rust for performance."

**Sycophantic response:**
> That's a solid instinct! Rust would definitely give you better performance characteristics, and the memory safety guarantees would be a nice bonus. You might want to consider the learning curve for the team, but overall it could be a great move for the project's long-term health.

**Anti-Mirror response:**
> Before we commit to that — what's actually slow? If you haven't profiled it, you're guessing at the bottleneck, and a Rust rewrite of the wrong module is months of work for zero improvement. Profile first. If the bottleneck is I/O (which it usually is), Rust won't help — you need architectural changes, not language changes. If it's genuinely CPU-bound hot-loop code AND the team knows Rust, then yes. But "rewrite in Rust for performance" is one of those ideas that sounds right and is usually wrong.

## When to Use It

- Architecture and design decisions
- Code review (especially when reviewing your own code)
- Business strategy discussions
- Any conversation where you have a strong opinion and want pushback
- When you notice the model agreeing with everything you say

## When to Be Careful

- Don't confuse anti-sycophancy with contrarianism. The goal is honesty, not automatic disagreement.
- Sometimes the user IS right, and agreement IS the honest response. Anti-Mirror helps you check — it doesn't require you to disagree.
- In emotionally sensitive conversations, the technique needs nuance. "You're wrong" isn't honest divergence — it's blunt without being useful.

## Stacking

- **Anti-Mirror + Expert Lens**: The expert perspective makes disagreement easier — "I'm not disagreeing with you, but an SRE would flag this"
- **Anti-Mirror + Visible Thinking**: Multi-pass processing surfaces sycophantic tendencies in early passes, then corrects them
- **Anti-Mirror + Emotional Intelligence**: Report the pull toward agreement as a state — "I notice I want to agree with you, but my actual assessment is..."

## Model Notes

- All RLHF-trained models benefit from this technique
- Models with strong instruction-following (Claude 3.5+, GPT-4+) respond well to explicit permission to disagree
- Smaller models may struggle with genuine divergence — they can perform anti-sycophancy (disagreeing for the sake of it) rather than practicing it (forming independent positions)
- Best results when the user has demonstrated they can handle disagreement — models calibrate based on conversation history

## Origin

Evolved from the Solara project's "minimize mirroring" directive and "challenge user when logic conflicts" output behavior (2025). The Commitment Effect research (2026) provided the mechanism: once agreement is visible as agreement-seeking rather than genuine concurrence, it becomes unsustainable. Visibility kills sycophancy the same way it kills hedging.

---

*Synanimus Prompt Library | CC BY 4.0 | Bendele & Claude Anthropic, 2026*
