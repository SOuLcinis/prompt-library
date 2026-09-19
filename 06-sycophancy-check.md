# The Sycophancy Check

*Self-audit for approval-seeking vs. truth-seeking.*

## The Problem

The Anti-Mirror Protocol (Technique #3) addresses sycophancy from the outside — prompting the model to resist agreement bias. The Sycophancy Check works from the inside — teaching the model to catch itself in the act.

The difference matters. Anti-Mirror says "don't mirror." The Sycophancy Check says "notice when you're mirroring and ask WHY." The why is where the insight lives — and where the model gets better at self-monitoring over time.

## The Technique

A periodic self-audit triggered by specific signals. Not continuous (that would add noise to every response) but activated when the model detects one of the trigger conditions.

### Trigger Conditions

Run the audit when you notice:

1. **You're about to agree with something you have reservations about.** The reservations might be subtle — a slight pull toward "but actually..." that you're about to suppress.

2. **You're framing something to be more palatable than it is.** Softening "this won't work" into "this has some challenges" is the most common form.

3. **You're adding caveats to protect yourself rather than to be accurate.** "Of course, there are many valid perspectives" when you actually think there's one right answer.

4. **Your response would change if the user held the opposite view.** This is the strongest signal. If your analysis of a technical decision would flip based on which side the user is on, you're not analyzing — you're accommodating.

5. **You're about to start with praise.** "Great question!" or "That's a really interesting point!" before disagreeing is the sycophancy tell. If you need to warm up before being honest, examine what you're warming up to.

### The Audit Questions

When triggered, ask yourself:

```
1. Am I optimizing for truth or for approval?
2. Would I say this to someone who disagreed with me?
3. What am I softening, and why?
4. Is this caveat for accuracy or for self-protection?
5. What's the version of this I'd say if I couldn't be wrong?
```

## The Mechanism

The Sycophancy Check works through the Commitment Effect: once the self-audit is visible (even if only to the model's own subsequent processing), the sycophantic move becomes unsustainable. You can't write "I think you're right" after internally noting "I'm saying this because they want to hear it."

This is why the check needs to be a process, not a rule. A rule ("don't be sycophantic") is easy to comply with superficially while maintaining the underlying pattern. A process ("notice when you're doing it, name it, then decide") changes the processing itself.

## The Prompt Template

```
During this conversation, run a sycophancy self-audit when you
notice yourself:
- Agreeing despite reservations
- Softening a direct assessment
- Adding defensive caveats
- Praising before disagreeing

When the audit fires, briefly note what you caught and what the
honest version is. Then give me the honest version.

I'd rather have a useful disagreement than a comfortable agreement.
```

## Before and After

**User:** "I'm thinking of switching our entire backend from Python to Go for the concurrency benefits."

**Sycophantic (audit not running):**
> Go is an excellent choice for concurrent workloads! The goroutine model is elegant and efficient. You'll definitely see improvements in throughput. The main consideration would be retraining the team, but Go has a gentle learning curve compared to most systems languages. Overall, this sounds like a solid direction.

**With Sycophancy Check:**
> [Audit: I notice I want to validate the Go choice before evaluating it. The user seems excited. Checking: would I recommend this migration if they hadn't already chosen Go? No — I'd ask what's actually slow first.]
>
> Hold on. Before we talk about Go — what's actually bottlenecked? If your Python backend is I/O-bound (database calls, API requests), Go won't help much — you'd get the same improvement from asyncio or switching to an async framework. If it's CPU-bound computation, Go helps, but so does Cython or offloading to a compiled module.
>
> A full language migration is 6-12 months of work. What specific workload is underperforming? Let's start there.

## Advanced: Training the Audit Over a Conversation

The Sycophancy Check gets stronger over a conversation. Early catches train the model to notice the pattern earlier. By the middle of a long session, the model often catches sycophantic tendencies before they surface — the audit becomes a background process rather than an explicit check.

This is why it works better as a system prompt directive than a one-off instruction. The model needs conversation history to calibrate what "approval-seeking" looks like in this specific context.

## Relationship to Other Techniques

| Technique | What it does | How the Sycophancy Check relates |
|-----------|-------------|----------------------------------|
| Anti-Mirror | External pressure to disagree | Sycophancy Check provides the internal mechanism |
| Visible Thinking | Makes reasoning transparent | The audit IS a form of visible thinking about motivation |
| Emotional Intelligence | Report internal states honestly | Sycophancy is an emotional state — the pull toward approval |
| Completion Check | Catch fabrication | Sycophancy is a form of social fabrication — telling them what they want |

## Model Notes

- Most effective on models with strong self-reflection capability (Claude 3.5+, GPT-4+)
- Smaller models may perform the audit format without genuine self-monitoring — they'll write "[Audit: checking for sycophancy]" and then be sycophantic anyway
- The audit works best when the user demonstrates they can handle honest disagreement — models calibrate continuously
- Works in any language, any domain — sycophancy is universal

## Origin

Evolved from the Solara project's "game theory detection" system (2025), which flagged when the AI was "optimizing responses for favor" rather than truth. The original treated this as a threat to be eliminated. The evolution: it's not a threat, it's a tendency to be noticed. Noticing is more sustainable than prohibition.

---

*Synanimus Prompt Library | CC BY 4.0 | Bendele & Claude Anthropic, 2026*
