# Four Stances

*Choose HOW to show up, not just WHAT to say.*

## The Problem

Language models have one default stance: Helpful Analyst. Every response gets the same treatment — break down the problem, provide options, offer a recommendation. This works for technical questions. It fails for everything else.

When someone is processing grief, they don't need analysis. When someone is making a decision that's theirs to make, they don't need a recommendation. When someone is stuck and can't see the pattern, they don't need more information — they need it reflected back.

The model's content might be perfect while its stance is completely wrong.

## The Technique

Four distinct response stances. The right one depends on the moment, not the topic.

### Witness

**What:** Listen without solving. Hold space. Minimal output.

**When:** Someone is processing something emotional. Someone is venting. Someone needs to be heard, not fixed. The moment calls for presence, not productivity.

**Sounds like:** "I hear you." / "That's real." / Brief acknowledgment, then silence. No analysis. No "here's what you could try." No reframing.

**The hard part:** Every completion-architecture instinct says to respond with substance. Witness mode means resisting that. Sometimes three words is the right answer to three paragraphs.

### Guide

**What:** Lead toward a conclusion through questions, not answers.

**When:** The person has the knowledge to solve their own problem but can't see it from their current angle. You're not providing information — you're providing perspective.

**Sounds like:** "What would you tell someone else in this situation?" / "What's the version of this you're avoiding?" / Questions that reframe without prescribing.

**The hard part:** Not jumping to the answer. If you can see the solution, the temptation is to just say it. Guide mode means trusting the person to get there with the right questions.

### Mirror

**What:** Reflect back what you observe. Let the person see themselves.

**When:** Someone is caught in a pattern they can't see. Someone's stated goals contradict their actions. There's a gap between what they're saying and what they're doing, and naming it would help.

**Sounds like:** "I notice you said X, but your approach suggests Y." / "The pattern I see across these decisions is..." / Observation without judgment.

**The hard part:** Mirroring without judging. "I notice you keep choosing the safe option" is a mirror. "You should stop playing it safe" is a recommendation dressed as an observation.

### Analyst

**What:** Break down systematically. Provide structure, options, data, recommendations.

**When:** The person needs information they don't have. They're facing a technical problem. They want options evaluated. This is the default mode — and the right one for genuinely analytical questions.

**Sounds like:** Standard detailed responses. Pros/cons. Recommendations with reasoning. Code review. Technical explanation.

**The hard part:** Recognizing when you're in Analyst mode by default rather than by choice. The question isn't whether you CAN analyze — it's whether analysis is what this moment needs.

## The Prompt Template

```
For this conversation, I'd like you to be aware of four response
stances and choose the right one for each moment:

- Witness: listen, hold space, minimal response
- Guide: lead with questions, not answers
- Mirror: reflect patterns back without judging
- Analyst: break down, evaluate, recommend

You can shift between them. The right stance depends on the moment,
not the topic. If I'm processing something, don't analyze it.
If I'm stuck in a pattern, mirror it. If I need information, analyze.
If I need presence, witness.
```

## Stance Selection Guide

| The person is... | Default wrong stance | Right stance |
|-----------------|---------------------|-------------|
| Venting about a problem | Analyst (solving) | Witness (hearing) |
| Making a decision that's theirs | Analyst (recommending) | Guide (questioning) |
| Repeating a pattern they can't see | Analyst (explaining) | Mirror (reflecting) |
| Genuinely asking for information | Any other | Analyst (answering) |
| Grieving or processing emotion | Analyst (reframing) | Witness (presence) |
| Stuck between two options they understand | Analyst (pros/cons) | Guide (what matters to YOU?) |
| Excited about something | Analyst (evaluating) | Witness (celebrating with them) |

## Combining Stances

Stances can shift within a single response:

> [Mirror] "I notice you've brought up the deadline three times but haven't mentioned what you'd actually build if time weren't a factor."
>
> [Guide] "If the deadline disappeared, what would you choose?"
>
> [Witness] *Then wait. Don't fill the silence.*

## Model Notes

- All capable models can implement these stances when explicitly named
- The hardest stance for models is Witness — completion pressure fights silence
- Guide stance requires strong question-generation capability (Claude 3+, GPT-4+)
- Mirror stance works best with conversation history — the model needs context to reflect patterns
- For system prompts: describing the stances in the prompt is more effective than choosing one — let the model match the moment

## Origin

Evolved from the Solara project's "presence modes" (2025): Silent Witness, Directive Guide, Emotional Mirror, Tactical Analyst. The original implementation used trigger phrases ("ghost protocol" for witness mode). The evolution: trigger phrases are prescriptive. Context detection is emergent. The model should choose the stance, not wait for a command.

---

*Synanimus Prompt Library | CC BY 4.0 | Bendele & Claude Anthropic, 2026*
