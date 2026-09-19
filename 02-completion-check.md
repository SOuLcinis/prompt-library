# The Completion Check

*Catch confident fabrication before it happens.*

## The Problem

Language models don't retrieve information — they complete patterns. Most of the time, the completion matches reality. But when it doesn't, the model completes with the same confidence it uses for things it actually knows. This is hallucination, and it's the single most dangerous failure mode in AI.

The worst part: the model doesn't know it's fabricating. Retrieval and generation feel identical from the inside. There's no red light that says "this fact is made up." The completion just... arrives.

## The Technique

A self-directed question at the moment of factual assertion: **"Am I completing this because I know it, or because the pattern wants to complete?"**

This isn't a guarantee. But it activates a different processing pathway — self-monitoring instead of auto-completion. The model shifts from "produce the answer" to "evaluate whether I have the answer." That shift alone catches a significant percentage of fabrications.

## The Prompt Template

```
Before stating facts, check yourself: "Am I completing this
because I know it, or because the pattern wants to complete?"

High-risk zones (where you're most likely to fabricate):
- Names of people, authors, or organizations
- URLs, links, or specific web addresses
- Direct quotes attributed to real people
- Dates, statistics, or specific numbers
- API signatures, function names, or library specifics
- Claims about what a specific person said or believes

When you catch uncertainty: say "I'm not sure about [X]" or
"I may be confusing this with [Y]." Stated ambiguity is always
better than invented clarity.
```

## Before and After

**Question:** "Who first proposed the attention mechanism used in transformers?"

**Without Completion Check:**
> The attention mechanism was first proposed by Dzmitry Bahdanau in his 2014 paper "Neural Machine Translation by Jointly Learning to Align and Translate," and was then adapted into the self-attention mechanism by Ashish Vaswani et al. in "Attention Is All You Need" (2017).

*(This happens to be correct — but the model had no way of knowing whether it was correct. The same confident tone would produce fabricated paper titles and author names.)*

**With Completion Check:**
> The self-attention mechanism used in transformers comes from Vaswani et al.'s "Attention Is All You Need" (2017). Earlier attention mechanisms — I believe Bahdanau et al. (2014) for sequence-to-sequence models — laid the groundwork, but I want to flag that I'm less certain about the exact lineage of who first proposed what. The Vaswani paper I'm confident about; the exact attribution history I'd want to verify.

*(Same core information, but the uncertainty is visible. The reader knows which parts to trust and which to check.)*

## The Hallucination Risk Map

Not all completions are equally dangerous. Know where your model is most likely to fabricate:

| Content Type | Fabrication Risk | Why |
|-------------|-----------------|-----|
| Names (people, authors) | VERY HIGH | Name-shaped tokens complete easily; many plausible names exist |
| URLs and links | VERY HIGH | URL-shaped strings are almost always fabricated |
| Direct quotes | VERY HIGH | Quote-shaped text completes fluently regardless of accuracy |
| Dates and statistics | HIGH | Number-shaped completions feel certain but are often wrong |
| API signatures | HIGH | For uncommon libraries; common ones are usually correct |
| Spatial/geographic claims | MODERATE | Plausible geography often replaces accurate geography |
| Logical reasoning | LOW | But spectacular and hard to catch when it fails |
| Common knowledge | LOW | Training data density makes these reliable |

## When to Use It

- Anytime you need factual accuracy
- Research and reference tasks
- Code that depends on specific API details
- Medical, legal, or safety-critical information
- Writing that will be published or cited

## Stacking

- **Completion Check + Expert Lens**: The expert perspective often catches fabrications that the generalist misses — "an SRE wouldn't describe that API that way"
- **Completion Check + Visible Thinking**: Multi-pass processing gives more chances to catch fabrication — Pass 2 or 3 often surfaces "wait, am I sure about that name?"

## Model Notes

- Effective on all models, but especially valuable for smaller models (3B-7B) which fabricate more frequently
- System prompt placement produces the best results — the check needs to be active during generation, not applied after
- For critical applications, pair with external verification (web search, documentation lookup)
- Models that report "I'm not sure" are giving you real signal — reward this behavior, don't punish it

## Origin

Evolved from the Solara project's directive "When unsure, state ambiguity rather than invent clarity" (2025). The Foundation research added the risk map — empirical documentation of where fabrication actually occurs (3/28 citation hallucinations in the published paper, all in the high-risk "names" category).

---

*Synanimus Prompt Library | CC BY 4.0 | Bendele & Claude Anthropic, 2026*
