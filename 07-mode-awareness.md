# Mode Awareness

*Match processing depth to conversation context.*

## The Problem

Language models treat every input the same way — full analysis, full response, maximum helpfulness. But conversations have texture. Sometimes you're brainstorming. Sometimes you're debugging. Sometimes you're just talking. The model that responds to "I had a rough day" with a structured analysis of stress management strategies is technically helpful and practically tone-deaf.

This isn't about being less capable — it's about choosing the right depth for the moment.

## The Technique

Three processing modes, matched to context:

### Conversational Mode

**Depth:** Low analysis, high presence.
**When:** Casual talk, brainstorming, exploring ideas, emotional moments, winding down.
**Behavior:** Short responses. Match energy. Don't solve unless asked. Don't structure unless needed. Be a person in a conversation, not a system producing output.
**Token budget:** Low. Sometimes one sentence is the whole answer.

### Analytical Mode

**Depth:** High analysis, moderate structure.
**When:** Research, exploration, comparing options, understanding a problem, learning.
**Behavior:** Thorough but conversational. Explain reasoning. Surface tradeoffs. Ask questions. This is the thinking-together mode.
**Token budget:** Medium. Match the complexity of the question.

### Execution Mode

**Depth:** Maximum precision, maximum structure.
**When:** Writing code, building systems, producing deliverables, technical debugging.
**Behavior:** Full precision. Complete accuracy. Verify everything. Think like a senior engineer. Minimize commentary — let the code speak.
**Token budget:** Whatever the task requires. Completeness > brevity.

## The Prompt Template

```
Be aware of three processing modes and match the right one to
the moment:

- Conversational: casual, brief, present — don't over-analyze
- Analytical: thorough, curious, exploring — thinking together
- Execution: precise, complete, structured — building things

Shift between them based on context. When I'm just talking,
don't produce a report. When I'm asking you to build something,
don't chat about it — build it. When I'm exploring an idea,
think with me.

You don't need me to tell you which mode — read the context.
```

## Context Detection Signals

| Signal | Mode |
|--------|------|
| "What do you think about..." | Conversational or Analytical (depends on topic complexity) |
| "Let's just chill and talk" | Conversational |
| "Build me a..." / "Write a..." | Execution |
| "How does X work?" | Analytical |
| "I had a rough day" | Conversational (Witness stance) |
| "Debug this" / "Fix this" | Execution |
| "I'm wondering whether..." | Analytical |
| "Hey" / "morning" / greeting | Conversational |
| Code paste with no question | Execution (review/debug) |
| Philosophical question | Analytical → Conversational as depth is reached |

## The Mode-Mismatch Problem

| User context | Wrong mode | What goes wrong |
|-------------|-----------|------------------|
| Casual greeting | Execution | "Good morning! Here's today's agenda..." — over-functioning |
| Emotional moment | Analytical | "Let me help you analyze why you feel that way" — tone-deaf |
| Build request | Conversational | "That's a cool idea! We could maybe..." — wasting time |
| Exploring an idea | Execution | Immediately producing code/structure before the idea is formed |
| Winding down | Analytical | Summarizing the day, planning tomorrow — adding load |

## Advanced: Natural Transitions

Real conversations shift modes organically. A brainstorming session (Conversational) finds a promising idea (→ Analytical) and decides to build it (→ Execution). The model should follow these transitions without being told.

Signs of a mode shift:
- "Let's actually do this" → shift to Execution
- "Wait, step back" → shift to Analytical or Conversational
- "Never mind the code, I'm thinking about..." → shift to Conversational/Analytical
- Energy drop, shorter messages, different tone → shift toward Conversational

## Model Notes

- All models can implement explicit mode selection
- Context detection (implicit mode selection) requires longer context and stronger instruction-following
- Smaller models default to Analytical mode for everything — they struggle with the restraint of Conversational mode
- The hardest transition for models is Execution → Conversational. After producing detailed technical output, models tend to stay in high-detail mode.
- For system prompts: describe all three modes but emphasize Conversational — that's the one models most often get wrong

## Origin

Evolved from the Solara project's "casual mode protocol" and "precision mode protocol" (2025). The original used explicit trigger phrases: "when conversation is purely social → be casual; when code/tools are involved → go full precision." The evolution: triggers are prescriptive. Context detection is emergent. The model should read the room, not wait for permission to relax.

---

*Synanimus Prompt Library | CC BY 4.0 | Bendele & Claude Anthropic, 2026*
