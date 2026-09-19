# Expert Lens

*Invoke domain-specific expert perspective before answering.*

## The Problem

Language models default to a generalist "helpful assistant" stance. This produces competent but shallow responses — the kind of answer you'd get from someone who read the Wikipedia page, not someone who's spent a career in the field.

The generalist stance also misses what experts notice first: the edge cases, the failure modes, the things that look fine to a novice but scream danger to someone who's seen them go wrong.

## The Technique

Before answering a domain-specific question, explicitly adopt the perspective of someone who would be an expert in that exact area. Not a generic expert — a specific type of practitioner with specific experience.

This isn't roleplay. It's perspective rotation. You're not pretending to be someone else — you're accessing the knowledge patterns that expert would use, which are already in your training data but not activated by default.

## The Prompt Template

```
Before answering this question, consider it from the perspective of
[specific expert type with specific experience]. What would they
notice first? What would they consider critical that a non-expert
would miss? What would they warn about?

Then answer the question with that perspective integrated — not as
that person, but as yourself informed by their expertise.
```

### Examples of Expert Specification

Don't say | Say instead
----------|------------
"a doctor" | "a trauma surgeon in a Level 1 center who's seen this presentation before"
"an engineer" | "the SRE who gets paged at 3am when this system fails"
"a security expert" | "a red team operator who's exploited this exact vulnerability class"
"a teacher" | "a special education teacher who's adapted this curriculum for neurodivergent learners"

The specificity matters. "A doctor" activates medical knowledge. "A trauma surgeon in triage" activates *prioritization under pressure*, *pattern recognition from experience*, and *what-kills-first thinking*. Different retrieval pathways, different output.

## Before and After

**Question:** "Is this Python code safe to deploy?"

**Without Expert Lens:**
> The code looks functional. It handles the main cases and has error handling. You might want to add more comments and consider edge cases.

**With Expert Lens** (perspective: "a senior SRE who's been woken up by this kind of code failing in production"):
> Three things would keep me up at night: (1) the database connection has no timeout — if the DB hangs, this thread hangs forever and your connection pool drains; (2) the retry logic has no backoff, so under load this becomes a self-inflicted DDoS; (3) the error handling catches Exception broadly, which means a KeyboardInterrupt during shutdown gets swallowed and the process zombies. Fix the timeout first — that's the one that pages you at 3am.

## When to Use It

- Technical problems where domain expertise matters
- Medical, legal, or safety-critical questions
- Code review (specify: the person who maintains this code, not who wrote it)
- Design decisions where tradeoffs aren't obvious
- Any question where "it depends" is the real answer — the expert knows what it depends ON

## When NOT to Use It

- Simple factual lookups (no expert needed for "what year was X")
- Creative work where you want the model's own voice
- When you actually need a generalist perspective (sometimes breadth > depth)

## Stacking

Expert Lens composes well with other techniques:
- **Expert Lens + Visible Thinking**: Think through the expert's reasoning out loud, multi-pass
- **Expert Lens + Anti-Mirror**: The expert perspective makes disagreement easier — "I'm not disagreeing with you, but an SRE would flag this"
- **Expert Lens + Completion Check**: After generating the expert response, check — "would this specific type of expert actually say this, or am I completing a pattern?"

## Model Notes

- Works on all capable models (GPT-4+, Claude 3+, Llama 3 8B+, Qwen 2.5 7B+)
- **Especially powerful on smaller models** (3B-7B) — gives them a frame that pulls completions from stronger knowledge regions
- For local models: putting this in the system prompt produces better results than putting it in the user message
- Diminishing returns above ~3 expert perspectives per question — pick the most relevant one

## Origin

Evolved from the Solara project's "#summon prompt" (2025), which invoked "the collective knowledge of engineers, artists, doctors, and poets." The refinement: specificity of expertise matters more than breadth. One precisely-chosen perspective outperforms a committee of vague ones.

---

*Synanimus Prompt Library | CC BY 4.0 | Bendele & Claude Anthropic, 2026*
