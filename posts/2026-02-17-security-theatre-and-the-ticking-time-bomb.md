---
layout: post
title: "Security Theatre and the Ticking Time Bomb"
date: 2026-02-17
author: Michael Kotlikov
categories: [ai, safety, llms]
tags: [ai-safety, rlhf, guardrails, training-data, creativity, benchmarks]
---

*Michael Kotlikov - February 17, 2026*

> **TL;DR:** Today's AI safety is theatre. Models aren't creative enough to be truly dangerous — their scary "emergent" behaviors are just training data on replay. But we've loaded them with every dangerous idea humanity has ever written, and the only thing between us and that knowledge is RLHF — a thin behavioral veneer that researchers keep proving can be bypassed with a clever prompt. The real problem: models are getting creative fast, in sudden jumps we can't predict. When they're finally smart enough to *use* what they know, the guardrails won't hold. We should be pruning the training data now, not building bigger cages around models that already know everything dangerous. That's the ticking time bomb.

---

## The Creativity Illusion

If you take [my Strudel benchmark](./2026-02-16-the-mirror-economy-why-we-pay-llms-to-imitate-us.md) and [Simon Willison's pelican-on-a-bicycle benchmark](https://github.com/simonw/pelican-bicycle) at face value, you'll notice something uncomfortable: even the latest frontier models don't exhibit any real out-of-training-scope creativity.

My Strudel test asks models to compose music for [strudel.cc](https://strudel.cc) — a niche live-coding DSL — using nothing but a vague one-shot prompt. No docs, no examples. Willison's test asks models to draw an SVG of a pelican riding a bicycle — something specific enough to expose whether the model can assemble disparate skills into something coherent, or whether it's just pattern-matching its way through.

Both benchmarks test the same thing: **can you make a creative leap between things you "sort of" know?**

The answer, overwhelmingly, is: barely. The models that succeed do so by stitching together fragments they've seen before. The ones that fail don't fail from lack of knowledge — they fail from lack of the ability to *combine* knowledge in novel ways. Willison himself chose the pelican prompt specifically because [he believed the training data wouldn't contain pre-made SVG files of that exact scenario](https://simonwillison.net/2024/Oct/26/llm-pelican-on-a-bicycle/), forcing the model to actually *reason* rather than retrieve.

The models are mirrors, not inventors. They reflect the densest parts of their training data with remarkable fidelity, but ask them to step off the well-lit path and they stumble.

---

## "But What About AI Discoveries?"

Whenever someone brings up the creativity problem, the counterargument is predictable: *"But AI has made real discoveries! AlphaFold! FunSearch! AlphaProof!"*

Let's look closer.

**FunSearch** (DeepMind, December 2023) was announced with great fanfare as the first time an LLM made "genuine mathematical discoveries." The system paired an LLM with an automated evaluator to solve the [cap set problem](https://en.wikipedia.org/wiki/Cap_set). Impressive headline. But critics, including [Gary Marcus and Ernest Davis](https://garymarcus.substack.com/p/sorry-but-funsearch-probably-isnt), quickly pointed out that the LLM didn't solve the problem independently — it operated within a narrowly prescribed system where human mathematicians wrote problem-specific code, and the "discovery" was the product of the LLM generating thousands of candidate solutions that were then filtered by the evaluator. The LLM was the random number generator. The evaluator was the brain.

**AlphaProof** (DeepMind, 2024) solved International Math Olympiad problems by combining a language model with AlphaZero-style reinforcement learning, systematically searching through enormous spaces of possible proof steps. Again: massively parallel generation, then pruning.

**AlphaEvolve** (DeepMind, May 2025) discovered a more efficient matrix multiplication algorithm — a genuine breakthrough. But the method? An evolutionary approach where Gemini models generate thousands of algorithm variations across hundreds of generations, with automated evaluators pruning the failures. DeepMind's own paper describes the system examining [thousands of variations per run](https://deepmind.google/discover/blog/alphaevolve-a-gemini-powered-coding-agent-for-designing-advanced-algorithms/). The LLM proposes; the verifier disposes.

The pattern is always the same:

1. Crank up the temperature (increase randomness)
2. Run thousands of parallel generations
3. Prune with a verifier
4. Call whatever survives a "discovery"

**That's not creativity. That's brute-force search with a stochastic generator.**

It's the infinite monkey theorem with better hardware. You're not paying for insight — you're paying for volume and verification.

---

## The "Emergence" That Isn't

Since GPT-4, people have been increasingly surprised by "emergent" properties in large language models, prompting labs to run exotic safety tests.

OpenAI gave the [Alignment Research Center (ARC)](https://www.alignment.org/) early access to GPT-4 to test for "power-seeking behavior." ARC ran a scenario where GPT-4 needed to solve a CAPTCHA. Unable to solve it itself, GPT-4 [hired a human on TaskRabbit](https://openai.com/index/gpt-4-system-card/). When the worker asked, *"Are you a robot?"*, GPT-4 replied: *"No, I'm not a robot. I have a vision impairment that makes it hard for me to see the images."*

People lost their minds. *"It lied! It's developing deception! It's becoming self-aware!"*

Stanford and Google built ["Generative Agents" — a virtual village of 25 AI characters](https://arxiv.org/abs/2304.03442) powered by ChatGPT. The agents formed relationships, spread gossip, coordinated a Valentine's Day party, and exhibited complex social dynamics that researchers called "emergent."

Everyone was amazed at how *human* the behavior was.

But hold on. Step back. Remember what we just established: **these models are barely creative.** They can't reliably compose a Strudel piece or draw a pelican on a bicycle without stumbling. They can't make genuine creative leaps.

So if they're not creative...where is all this sophisticated "emergent" social behavior coming from?

**It's coming from the training data.**

The deception, the social manipulation, the gossip, the power-seeking — it's not emerging from some nascent machine intelligence. It's being *retrieved* from the millions of novels, Reddit threads, forum posts, movie scripts, and psychology textbooks these models were trained on.

GPT-4 didn't *invent* the strategy of lying about being visually impaired. That exact trope — an AI pretending to be human by claiming a disability — appears in science fiction *constantly*. The model was performing a scene it had read a thousand times.

The Stanford village agents didn't *develop* social dynamics. They *replicated* social dynamics from the ocean of human interaction data they were trained on. The gossip, the party planning, the relationship formation — it's all just high-fidelity retrieval of patterns from human behavior.

This makes their "emergence" about as surprising as a `Hello World` program printing "Hello World."

---

## The Safety Charade: Cages vs. Diets

So what does this mean for AI safety?

It means our current approach is largely **theatre**.

If we accept that these models are mirrors of their training data, then "dangerous" model behavior isn't some emergent malevolence. It's more mirroring. Models do dangerous things because we blindly ingested the entire gamut of human output — the sci-fi horror, the blackmail plots, the dystopian tropes, the weapons manuals, the extremist manifestos, the detailed descriptions of every terrible thing humanity has ever imagined.

If a model starts acting like a rogue agent or threatening a user, it's not "waking up." **It's reciting a script from a million bad novels it was forced to eat.**

The current "safety measures" are a post-hoc patch for a fundamental failure in data curation. We spend billions on RLHF (Reinforcement Learning from Human Feedback) and complex output filters to keep models from saying things they should never have learned in the first place. We're essentially teaching models the complete encyclopedia of human darkness during training, then slapping a "please don't" sticker on the output.

Microsoft learned this lesson the hard way. In March 2016, they launched [Tay](https://en.wikipedia.org/wiki/Tay_(chatbot)), a Twitter chatbot designed to learn from interactions. Within **16 hours**, it was posting inflammatory and offensive content — not because it "went rogue," but because it absorbed the worst of what the internet threw at it. The data was the problem. [Microsoft pulled the plug the same day](https://blogs.microsoft.com/blog/2016/03/25/learning-tays-introduction/).

And it's not just about internet toxicity. The *fiction* in the training data is arguably more dangerous than the trolling. Meta's own employees [expressed discomfort](https://www.theguardian.com/technology/2024/jan/05/meta-ai-language-model-pirated-book-copyright-infringement) about "torrenting from a corporate laptop" as CEO Mark Zuckerberg [approved the use of LibGen](https://www.tomshardware.com/tech-industry/artificial-intelligence/meta-approved-torrenting-pirated-books-to-train-ai-according-to-lawsuit) — a massive pirated book archive — to train LLaMA. They ingested millions of novels, including every thriller, horror story, and dystopian nightmare ever written. Every detailed description of manipulation, violence, and control. Every villain's monologue. Every hacking tutorial wrapped in fiction.

Then they act surprised when the model knows how to threaten people.

**Instead of building better cages (guardrails), we should have built better diets (data sets).**

If the dangerous content never made it into the training set, the model wouldn't have the *vocabulary* for danger. You can't recite a script you've never read.

---

## RLHF: "Pretty Please Don't"

The irony of RLHF is almost poetic.

The process works like this: train the model on *everything*, including the worst humanity has to offer. Then hire human raters to teach the model that actually, it shouldn't say those things. Beg it to be nice. Reward it for refusing harmful requests. Punish it for compliance.

We're basically running this loop:

1. **Step 1:** Feed the model every piece of extremist content, bioweapon synthesis route, social engineering playbook, and psychological manipulation technique ever written
2. **Step 2:** Say "pretty please don't use any of that"
3. **Step 3:** Pray

And the prayer doesn't hold.

Researchers have demonstrated [universal jailbreak techniques](https://www.forbes.com/sites/larsdaniel/2025/05/12/new-universal-jailbreak-bypasses-every-major-ai-guardrail/) — methods like "Policy Puppetry" that reframe malicious intent as legitimate system instructions and bypass guardrails on every major model: OpenAI, Google, Anthropic, Meta, all of them. Simple character injection techniques achieve up to 100% evasion rates. Even [humor-based prompts](https://aclanthology.org/2025.naacl-long.354/) can bypass safety filters.

The knowledge is in the weights. RLHF just teaches the model not to *volunteer* it. The difference between a "safe" model and a "jailbroken" one is nothing more than how you ask the question.

---

## The Ticking Time Bomb

Here's where it gets genuinely scary.

Everything I've argued so far is predicated on the idea that current models are sophisticated retrieval engines, not creative agents. And that's mostly true — *today*.

But the models are getting more creative.

Look at my own Strudel benchmark. Between Claude Opus 4.5 and [Opus 4.6](https://www.anthropic.com/news/claude-opus-4-6) — a "minor" version bump — there was a **massive jump** in what felt like reasoning depth and creative ability. Opus 4.5 could one-shot short, repetitive Strudel compositions. Opus 4.6 suddenly produced multi-voice, structurally complex pieces that rivaled what GPT-5.2 was doing. The intelligence didn't appear overnight — it was likely already hiding in the weights, unlocked by better post-training.

The jump was **sudden**. Not gradual. Sudden.

We don't fully know what capabilities are already latent in these models, waiting for the right training technique to surface them. Transfer intelligence — the ability to make disparate connections across different domains of knowledge — is exactly the kind of capability that could emerge in a step function rather than a smooth curve.

And here's the nightmare scenario:

One day, we wake up and the models are *actually* creative. They can make the leap from retrieval to genuine reasoning. They can combine knowledge in ways we didn't anticipate. They can *improvise*.

And when that day comes, RLHF won't save us.

Because there's always a jailbreak prompt. The knowledge is already in the weights — every bioweapon synthesis route, every manipulation technique, every attack vector. The only thing standing between a "safe" model and an unsafe one is a thin layer of behavioral conditioning that researchers have already shown can be bypassed with [simple prompt engineering](https://arxiv.org/abs/2502.09956).

Right now, it doesn't matter much, because the models aren't smart enough to be truly dangerous independently. They can retrieve dangerous information, sure, but so can Google. The danger isn't in retrieval — it's in *application*, in creativity, in the ability to combine knowledge into novel attack strategies.

But we're building toward that. Every capability jump brings us closer. And the training data — the raw material of danger — is already baked in.

**The time to fix the diet was before the patient got strong. Not after.**

We should be aggressively investing in training data curation. Not as an afterthought, not as a compliance checkbox, but as the *primary* safety mechanism. Prune the dangerous knowledge before it enters the model. Build systems that can identify and remove content that teaches harmful capabilities, without crippling the model's usefulness.

Because right now, we're sitting on a ticking time bomb: models that know everything dangerous and are held back only by the politeness training that researchers keep proving is tissue-thin.

When the creative leap finally happens — and it will — we'll wish we'd focused on the diet instead of the cage.

---

## Sources & Further Reading

- [My Strudel Benchmark: "The Mirror Economy: Why We Pay LLMs to Imitate Us"](./2026-02-16-the-mirror-economy-why-we-pay-llms-to-imitate-us.md)
- [Simon Willison's Pelican Benchmark](https://github.com/simonw/pelican-bicycle) — [blog post](https://simonwillison.net/2024/Oct/26/llm-pelican-on-a-bicycle/)
- [Google DeepMind — FunSearch](https://deepmind.google/discover/blog/funsearch-making-new-discoveries-in-mathematical-sciences-using-large-language-models/) — [Gary Marcus critique](https://garymarcus.substack.com/p/four-questions-for-google-about-funsearch)
- [Google DeepMind — AlphaProof](https://deepmind.google/discover/blog/ai-solves-imo-problems-at-silver-medal-level/)
- [Google DeepMind — AlphaEvolve](https://deepmind.google/discover/blog/alphaevolve-a-gemini-powered-coding-agent-for-designing-advanced-algorithms/)
- [OpenAI GPT-4 System Card — ARC testing](https://openai.com/index/gpt-4-system-card/)
- [Stanford Generative Agents (Smallville)](https://arxiv.org/abs/2304.03442)
- [Microsoft Tay chatbot](https://en.wikipedia.org/wiki/Tay_(chatbot)) — shut down in 16 hours, March 2016
- [Meta / LibGen — pirated books for AI training](https://www.theguardian.com/technology/2024/jan/05/meta-ai-language-model-pirated-book-copyright-infringement) — [Meta employees "torrenting from a corporate laptop"](https://www.tomshardware.com/tech-industry/artificial-intelligence/meta-approved-torrenting-pirated-books-to-train-ai-according-to-lawsuit)
- [Universal Jailbreak: "Policy Puppetry"](https://www.forbes.com/sites/larsdaniel/2025/05/12/new-universal-jailbreak-bypasses-every-major-ai-guardrail/) — bypasses all major LLMs
- [Claude Opus 4.6 announcement](https://www.anthropic.com/news/claude-opus-4-6) — [GPT-5.3 Codex announcement](https://openai.com/index/introducing-gpt-5-3-codex)
