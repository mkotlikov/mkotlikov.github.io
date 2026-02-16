It started with a distraction—specifically, an ad for Brain.fm. I was fascinated by their claim of using rapid volume modulation to hack focus, so naturally, instead of doing my actual work, I decided to reverse-engineer it.

I’m not a musician. My relationship with music usually involves finding a single track in a movie soundtrack and looping it until I absolutely resent it. But I *am* a programmer. So, I built a quick in-browser focus app ([focus.nemitek.com](https://focus.nemitek.com)).

Brain.fm pays real composers to write their underlying tracks. I don't have that skill or budget. But a friend turned me onto [Strudel.cc](https://strudel.cc), a live-coding environment that ports the TidalCycles pattern language into JavaScript.

**And that’s when I realized I had the perfect Turing test.**

Think about what an LLM actually knows. These models have ingested centuries of music theory textbooks. They know the circle of fifths, they’ve parsed millions of MIDI files, and they understand the mathematical structure of a Bach fugue. They possess the *domain knowledge*.

But Strudel is a niche, functional language with very little training data online. The models haven't memorized enough of it to cheat.

To write a Strudel composition, an AI can't just autocomplete code it saw on GitHub. It has to perform a high-wire act of **transfer learning**: it must take its deep, abstract understanding of music theory and translate it, in real-time, into a syntax it barely recognizes. It has to figure it out using logic, not memory.

I put the heavy hitters to the test with a single prompt: `make a classical composition for strudel.cc`.

## The Stochastic Parrot Phase

I started with **Gemini 3 Flash**, which Google markets as their premier coding engine.

It was a disaster. It didn't just fail; it failed because it couldn't reason. It clearly "knew" the syntax existed—it was trying to use valid Strudel functions—but it couldn't connect the dots. It took 9 iterations to get code that didn't crash, and even then, the result was pure silence.

I then tried **Gemini 3 Pro**. It was a grind. It took two full iterations of back-and-forth prompting just to get a short, functional loop running. It wasn't that the model was "dumb"—it clearly knew the syntax existed—but it couldn't reason through the structure without hand-holding. It had the puzzle pieces, but it didn't know how to fit them together.

If I had stopped here, my conclusion would have been cynical: *LLMs are just stochastic parrots. There is no Strudel in the training set, so they fail.*

## The "Smart" Ghost: GPT-5.2 & Codex

Then I tried **GPT-5.2** and **GPT-5.2 Codex**. This was the shock.

They didn't just one-shot the code; they wrote complex, multi-voice compositions that sounded like actual video game MIDI tracks. They handled the functional syntax effortlessly. It proved that **General Intelligence is real.** These models successfully transferred logic from other domains to a language they barely knew.

And then there was **Claude Opus 4.5**. It also one-shotted the code, but the results were simpler—technically correct, but repetitive and short. It lacked the "ghostly" reasoning depth I saw in the OpenAI models.

## The Market Paradox: Why We Chose Sonnet 4.5

But here is the fascinating contradiction. throughout late 2025, while GPT-5.2 was demonstrating this superior reasoning capability, the developer world (myself included) was obsessed with **Claude Sonnet 4.5**.

We voted with our wallets for Sonnet, even though my tests show it was *less* generally intelligent than GPT-5.2. Why?

**Because right now, we value Data over Intelligence.**

Sonnet 4.5 "vibed" better. It was trained on a massive corpus of the tedious, repetitive code we write every day (React components, Python scripts, SQL queries). It was a better **Mirror** of our daily grind. GPT-5.2 was "smarter"—it could figure out new things—but for 99% of our jobs, we don't need a genius to figure out new things. We need a really fast intern to do the boring things we already know how to do.

We acknowledge the Ghost, but we pay for the Mirror.

## The Unlock: The Lesson of Opus 4.6

Just as I was finalizing these thoughts, **Claude Opus 4.6** and **GPT-5.3 Codex** dropped on February 5th, 2026. The shift was subtle but profound.

Opus 4.6 is a "minor" version upgrade, yet it unlocked a massive jump in capability, suddenly matching the reasoning depth of the GPT-5 class. This suggests something incredibly important about how these models work. 

The intelligence didn't just appear overnight. It was likely **hiding in the weights** of Opus 4.5 all along. The base model had the capacity, but it took refined Post-Training and RLHF (Reinforcement Learning from Human Feedback) to unlock it. We aren't just teaching them new facts; we are learning how to access the reasoning capabilities that are already there, dormant.

## The Conclusion: It’s Early Days

My test results point to a clear reality: **LLMs do think, and they do reason, but it is very early days.**

While GPT-5.3 Codex can write a beautiful string quartet snippet, no model could generate a full, multi-minute song with structural progression. The reasoning is brittle. It can sprint, but it can't run a marathon.

We are currently in a phase where we prioritize the utility of the Mirror—the ability to recall and format vast amounts of data. But the reasoning capability is real, it is emergent, and it is growing. The fact that a minor version update can "unlock" such a leap in quality suggests that we haven't even scratched the surface of what these current weights are capable of.

The intelligence isn't missing. It's just waking up.