---
layout: post
title: "Mirrors, Not Ghosts: The Intelligence Is in the Data, Stupid"
date: 2026-02-16
author: Michael Kotlikov
categories: [ai, llms, music, coding]
tags: [strudel, brainfm, gpt, claude, gemini, grok, benchmarks]
---

I didn’t set out to write a blog post about frontier-model generalization. I set out to procrastinate better.

It started with a **brain.fm** ad. I’ve always been curious about binaural beats, but what caught my attention wasn’t “binaural” so much as this *aggressive, fast volume modulation* thing they do—almost like a tremolo you can feel in your skull. My brain immediately did the classic developer move:

> “I can probably build a jankier version of that.”

So I did. I built a little in-browser focus app: **https://focus.nemitek.com**.

Brain.fm pays musicians and then runs algorithms on their music. I do not pay musicians (tragically), so I tried procedural music. Then I added settings. Then feature creep turned it into a small spaceship control panel. And eventually I hit a wall:

**How do I code “real music” that doesn’t sound like a calculator doing slam poetry?**

A friend turned me on to **strudel.cc**, and it felt like destiny. Strudel is a live-coding music environment (pattern-based, JavaScript-y, super fun). And I had a very 2026 thought:

> “Any LLM should be able to vibe this.”

So I ran an experiment.

---

## The experiment: “make a classical composition for strudel.cc” (one-shot)

I used a single prompt:

**“make a classical composition for strudel.cc”**

No docs. No examples. No “here’s the syntax.” Just: *show me you can generalize.*

This wasn’t really a music test. It was a **transfer test**:

- can you take music knowledge (common in training)
- and translate it into a niche DSL (probably rare in training)
- without face-planting?

It’s the same kind of vibe as Simon Willison’s wonderfully weird benchmark:

> **“Generate an SVG of a pelican riding a bicycle.”**  
> <https://github.com/simonw/pelican-bicycle>

It’s not that pelicans or bicycles are impossible. It’s that the task is *specific enough* to expose whether the model can assemble skills it “sort of” has into something coherent—especially off the well-lit path.

Strudel became my pelican.

---

## Results

### Gemini 3 Flash

This was my “BIG mistake” model.

When it didn’t throw syntax errors, it produced something even funnier: **silence**. Code that looked plausible, executed, and did… nothing. Or it ran but needed so much iteration that I felt like I was teaching it Strudel one paper cut at a time.

In my testing: **completely useless** for this task.

### Gemini 3 Pro

Better, but still not a one-shot machine for me.

With 1–3 rounds of back-and-forth, I could usually get a short, pleasant snippet. Once it *worked*, it could sound nice! But it rarely landed on a playable “composition” immediately.

### Opus 4.5

This is where the vibe changed.

Opus 4.5 would **one-shot working Strudel** reliably. The compositions tended to be on the shorter/repetitive side, but the important thing happened: it crossed the threshold from “arguing with the tool” to “playing with the tool.”

### Sonnet 4.5

Sonnet 4.5 lived in the uncanny valley for this experiment.

Sometimes it hit. Sometimes it ran but felt musically thin. Sometimes it wandered into “technically patterns” without really composing. It was clearly less consistent than Opus 4.5 in my Strudel test… and that fact is about to matter a lot, because…

### GPT-5.2

GPT-5.2 was my “wait, what?” moment.

It reliably one-shot working code, and the results were usually:

- longer  
- more layered  
- more structured  
- more “composition” than “demo loop”

This is the point where my initial cynical take (“LLMs can only do what’s in their training set”) started wobbling.

### GPT-5.2 Codex

Same story, often even more “composed.”

Depending on the run, GPT-5.2 or 5.2 Codex would win, but both consistently gave me the best combination of **works-first-try + substantial output**.

---

## The Market Paradox: Why We Chose Sonnet 4.5

Here’s the fascinating contradiction.

Throughout late 2025—while GPT-5.2 was, in my testing, demonstrating **superior generalization**—the developer world (myself included) was obsessed with **Claude Sonnet 4.5**.

Sonnet 4.5 launched September 29, 2025 and became *the* “default coding model” vibe for a lot of people.  
<https://support.claude.com/en/articles/12138966-release-notes>

But my Strudel test strongly suggested Sonnet 4.5 was **less generally intelligent** than GPT-5.2.

So why did we collectively vote with our wallets for Sonnet?

Because right now, we value **Data over Intelligence**.

Sonnet 4.5 “vibed” better for real work because it was an incredible **Mirror** of our daily grind—React components, Python scripts, SQL queries, the repetitive stuff we write all day. It didn’t need to be a genius. It needed to be a *fast, reliable intern* that could do the boring parts at scale.

GPT-5.2 felt “smarter”—more capable when you step off the path. But for 99% of production work, we’re not asking the model to invent a new language or bridge music theory into a niche DSL. We’re asking it to:

- refactor code  
- write glue  
- generate endpoints  
- fix tests  
- make the tenth similar component

So yeah:

**We acknowledge the Ghost, but we pay for the Mirror.**

---

## Ghosts vs mirrors (why I’m stealing Karpathy’s ghost and renaming it)

Andrej Karpathy has a metaphor I love: LLMs aren’t “animals,” they’re more like **ghosts**—statistical distillations of humanity’s text, eerie and powerful, but not embodied in the world.

(Reference: Karpathy’s “Animals vs Ghosts” essay)  
<https://karpathy.bearblog.dev/animals-vs-ghosts/>

That metaphor lands.

But after this Strudel adventure, my vibe is: **mirrors** are the more useful mental model day-to-day.

These systems reflect what humans do a lot of:

- common stacks  
- common patterns  
- common formats  
- common bugs  
- common tedious work

Where the data is dense, the mirror is crisp.

Where the data is sparse—hello, Strudel—the mirror gets blurry. And that blur is exactly what I was testing.

There *are* sparks of real connection-making (music theory → structure → timing → synthesis), but the boundary of competence still smells like the boundary of the training diet.

---

## Epilogue: February 5th, 2026, two drops ~20 minutes apart

Just as I was finalizing these thoughts, **Claude Opus 4.6** and **GPT-5.3 Codex** dropped on **February 5th, 2026**.

Anthropic announcement:  
<https://www.anthropic.com/news/claude-opus-4-6>

And things got… interesting.

### Opus 4.6

Opus 4.6 felt like a real jump. Not a “new vibe,” but a *capability* shift: longer, more confident, more sustained structure—suddenly operating in the tier I’d associated with the GPT-5 class.

Anthropic frames it as better planning, longer agentic tasks, better reliability in larger codebases, and improved debugging/review.

### Codex 5.3

Codex 5.3, in my runs, took another step. The standout wasn’t just correctness—it was musical “taste.” It stepped away from pure electronic/MIDI demo energy and leaned into **strings** as a focal point in a way that felt more mature.

---

## The Unlock: The Lesson of Opus 4.6

Here’s the part that messed with my mental model:

Opus 4.6 is a “minor” version bump, yet it unlocked a huge jump in what felt like reasoning depth.

That suggests something important: the intelligence didn’t appear overnight. It was likely **already hiding in the weights**.

The base model may have had the capacity in Opus 4.5, but it took refined post-training—alignment, preference optimization, RLHF-style shaping—to reliably **access** that capability.

In other words: we’re not just teaching models new facts.

We’re learning how to *pull* the best thinking that’s already in there out to the surface, consistently.

And that’s wild, because it reframes progress: sometimes the “new model” isn’t a bigger brain—sometimes it’s a better way to **use** the brain you already had.

---

## My rankings

### Ranking before the epilogue (late 2025 / early 2026 testing)

1. **OpenAI GPT-5.2 / GPT-5.2 Codex** (depending on the run, either could win)  
2. **Claude Opus 4.5** (consistent one-shot, compositions shorter)  
3. **Grok 4.1 Thinking** (not consistent one-shot, but occasional brilliant chaos)  
4. **Google Gemini 3 Pro** (never one-shot for me; decent once corrected)  
5. **Gemini 3 Flash** (nope tier for this benchmark)

### Ranking after Feb 5, 2026

1. **OpenAI Codex 5.3**  
2. **Anthropic Claude Opus 4.6**  
3. **xAI Grok Thinking 4.1**  
4. **Google Gemini 3 Pro**  
5. **Gemini 3 Flash** (still in time-out)

---

## Data section

*(I’ll paste raw runs here later: prompts, model settings, iteration counts, Strudel links, notes, and subjective ratings.)*

- Prompt(s) used:  
- Date(s) tested:  
- Model settings:  
- Run logs:  
- Strudel links:  
- Notes / observations:  
