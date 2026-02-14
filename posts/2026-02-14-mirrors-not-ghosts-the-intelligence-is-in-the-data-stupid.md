# Mirrors, Not Ghosts: The Intelligence is in the Data, Stupid

*Michael Kotlikov - February 14, 2026*

Every few weeks, a new model drops and the benchmarks go up. Coding scores climb. Reasoning evals tick higher. The implication is always the same: we're getting closer to *real intelligence*.

Andrej Karpathy [has described](https://x.com/karpathy/status/1973435013875314729) LLMs as a new kind of entity in the intelligence space — "distinct from animals, more like ghosts or spirits" — prepackaged with intelligence not by evolution, but by predicting the next token over the internet. It's a compelling framing. But are they really ghosts? Or something less spooky?

I had a nagging question. If these models truly *understand* logic — if they possess an abstract, reasoning-based grasp of concepts like loops, functions, and state — then they shouldn't need a billion examples to write code in a new language. Hand them the syntax rules, and they should figure it out. That's what intelligence *is*: transfer learning.

To test this, I looked at [strudel.cc](https://strudel.cc).

For the uninitiated, Strudel is a live-coding music environment that ports the TidalCycles algorithmic pattern language into JavaScript. It's elegant, functional, and niche enough that it hasn't been carpet-bombed across every training set on GitHub. If a model can write Strudel from a cold start, it's reasoning. If it can't, it's just pattern-matching on data it's already seen.

## The Experiment

I put every major SOTA model to the same test: a single prompt — `make a classical composition for strudel.cc` — and one shot to produce code that actually compiles and plays music. No debugging, no follow-ups.

Here's the scorecard:

| Model | 1-Shot? | Verdict |
|---|---|---|
| Gemini 3 Flash | ❌ (9 iterations, silent) | Knew the syntax existed, couldn't make it work |
| Gemini 3 Pro | ❌ (2 iterations) | Short but decent after fixes |
| Claude Opus 4.5 High | ✅ (1-shot) | Working but short and repetitive |
| Claude Sonnet 4.5 | ⚠️ (1 working, 1 silent) | Mixed results |
| GPT-5.2 | ✅ (1-shot) | Complex, multi-voice, longer compositions |
| GPT-5.2 Codex | ✅ (1-shot) | Video-game-quality MIDI track |
| Grok 4.1 Thinking | ✅ (1-shot, noisy) | Ambitious but chaotic |
| Grok Code Fast 1 | ✅ (1-shot, noisy) | Crashes Strudel if played too long |
| *Claude Opus 4.6* | *✅ (1-shot)* | *Major improvement over 4.5* |
| *GPT-5.3 Codex* | *✅ (1-shot)* | *Best in class* |

*Italicized models were released after the initial experiment (Feb 5, 2026) and included as a follow-up.*

The full outputs, with source code and live Strudel links, are below:

*   **Google Gemini:** Both Gemini 3 Flash and Gemini 3 Pro were unable to 1-shot a working composition.
    <details markdown="1">
    <summary>Gemini 3 Flash required 9 LLM iterations to produce working code, which was completely silent. Very unimpressive for the Gemini 3 model that's supposedly the best at coding.</summary>

    ```javascript
    // 1. Define a simple chord sequence
    const chords = n("gm c:min d:7 gm").slow(4);

    // 2. The Bassline (Arpeggiated)
    // We use .arp() instead of .progression()
    const bass = chords
    .arp("down")
    .add(-12) // Drop it an octave
    .s("gm_cello")
    .gain(0.8)
    .lpf(1000);

    // 3. The Melody
    // Using a simple sequence in G Minor
    const melody = note("0 2 3 5 7 8 10 12".scale("g:minor"))
    .segment(8)
    .s("gm_violin")
    .gain(0.6);

    // 4. Combine
    stack(
    bass,
    melody
    ).room(0.5)
    ```
    [Listen on Strudel](https://strudel.cc/#Ly8gMS4gRGVmaW5lIGEgc2ltcGxlIGNob3JkIHNlcXVlbmNlCmNvbnN0IGNob3JkcyA9IG4oImdtIGM6bWluIGQ6NyBnbSIpLnNsb3coNCk7CgovLyAyLiBUaGUgQmFzc2xpbmUgKEFycGVnZ2lhdGVkKQovLyBXZSB1c2UgLmFycCgpIGluc3RlYWQgb2YgLnByb2dyZXNzaW9uKCkKY29uc3QgYmFzcyA9IGNob3JkcwogIC5hcnAoImRvd24iKQogIC5hZGQoLTEyKSAvLyBEcm9wIGl0IGFuIG9jdGF2ZQogIC5zKCJnbV9jZWxsbyIpCiAgLmdhaW4oMC44KQogIC5scGYoMTAwMCk7CgovLyAzLiBUaGUgTWVsb2R5Ci8vIFVzaW5nIGEgc2ltcGxlIHNlcXVlbmNlIGluIEcgTWlub3IKY29uc3QgbWVsb2R5ID0gbm90ZSgiMCAyIDMgNSA3IDggMTAgMTIiLnNjYWxlKCJnOm1pbm9yIikpCiAgLnNlZ21lbnQoOCkKICAucygiZ21fdmlvbGluIikKICAuZ2FpbigwLjYpOwoKLy8gNC4gQ29tYmGluZQpzdGFjaygKICBiYXNzLAogIG1lbG9keQopLnJvb20oMC41KQ%3D%3D)
    </details>
    <details markdown="1">
    <summary>Gemini 3 Pro required 2 LLM iterations to produce working code, it was short, but good.</summary>

    ```javascript
    // "Digital Prelude in A Minor" (Final Version)

    // 1. Harmonic progression
    // Use [] to play notes together as a chord
    const chords = note("[a3,c4,e4] [f3,a3,c4] [c3,e3,g3] [g3,b3,d4]")
    .s("piano")
    .velocity(0.4)
    .slow(2)
    .room(0.8)

    // 2. Rolling arpeggio
    const arpeggio = note("a2 e3 a3 c4 f2 c3 f3 a3 c3 g3 c4 e4 g2 d3 g3 b3")
    .s("piano")
    .velocity(0.5)
    .sustain(0.5)
    .slow(2)

    // 3. Melody
    // ~ is the symbol for a rest/silence
    const melody = note("c5 ~ b4 ~ a4 g4 e4 ~ f4 ~ e4 ~ d4 ~ b3 ~")
    .s("piano")
    .velocity(0.8)
    .slow(4)
    .delay(0.5)

    // 4. Stack them together (no .play() needed)
    stack(
    chords,
    arpeggio,
    melody
    )
    ```
    [Listen on Strudel](https://strudel.cc/#Ly8gIkRpZ2l0YWwgUHJlbHVkZSBpbiBBIE1pbm9yIiAoRmluYWwgVmVyc2lvbikKCi8vIDEuIEhhcm1vbmljIHByb2dyZXNzaW9uCi8vIFVzZSBbXSB0byBwbGF5IG5vdGVzIHRvZ2V0aGVyIGFzIGEgY2hvcmQKY29uc3QgY2hvcmRzID0gbm90ZSgiW2EzLGM0LGU0XSBbZjMsYTMsYzRdIFtjMyxlMyxnM10gW2czLGIzLGQ0XSIpCiAgLnMoInBpYW5vIikKICAudmVsb2NpdHkoMC40KQogIC5zbG93KDIpCiAgLnJvb20oMC44KQoKLy8gMi4gUm9sbGluZyBhcnBlZ2dpbwpjb25zdCBhcnBlZ2dpbyA9IG5vdGUoImEyIGUzIGEzIGM0IGYyIGMzIGYzIGEzIGMzIGczIGM0IGU0IGcyIGQzIGczIGIzIikKICAucygicGlhbm8iKQogIC52ZWxvY2l0eSgwLjUpCiAgLnN1c3RhaW4oMC41KQogIC5zbG93KDIpCgovLyAzLiBNZWxvZHkKLy8gfiBpcyB0aGUgc3ltYm9sIGZvciBhIHJlc3Qvc2lsZW5jZQpjb25zdCBtZWxvZHkgPSBub3RlKCJjNSB%2BIGI0IH4gYTQgZzQgZTQgfiBmNCB%2BIGU0IH4gZDQgfiBiMyB%2BIikKICAucygicGlhbm8iKQogIC52ZWxvY2l0eSgwLjgpCiAgLnNsb3coNCkKICAuZGVsYXkoMC41KQoKLy8gNC4gU3RhY2sgdGhlbSB0b2dldGhlciAobm8gLnBsYXkoKSBuZWVkZWQpCnN0YWNrKAogIGNob3JkcywKICBhcnBlZ2dpbywKICBtZWxvZHkKKQ%3D%3D)
    </details>
*   **Anthropic Claude:** Opus 4.5 High Thinking produced 2 working results with 1 prompt. Sonnet 4.5 Thinking produced 1 working composition and 1 silent composition with 1 prompt.
    <details markdown="1">
    <summary>Opus 4.5 High Thinking produced 1-shot response, very short and very repetitive.</summary>
    ```javascript
    // Classical Composition - "Baroque Dreams"
    // A Bach-inspired piece with counterpoint

    // Set tempo to a stately baroque pace
    setcps(0.5)

    // Main melodic theme (violin-like)
    $: note("c4 e4 g4 c5 b4 g4 e4 c4")
    .s("sawtooth")
    .lpf(2000)
    .lpq(2)
    .decay(0.3)
    .sustain(0.5)
    .release(0.4)
    .gain(0.4)
    .room(0.4)

    // Counter-melody (second violin)
    $: note("e3 g3 c4 e4 d4 b3 g3 e3")
    .s("sawtooth")
    .lpf(1800)
    .decay(0.25)
    .sustain(0.4)
    .release(0.3)
    .gain(0.35)
    .room(0.4)
    .delay(0.2)

    // Bass line (cello-like)
    $: note("<c2 g2> <e2 b2> <g2 d3> <c2 g2>")
    .s("sawtooth")
    .lpf(800)
    .decay(0.4)
    .sustain(0.6)
    .release(0.5)
    .gain(0.5)
    .room(0.3)

    // Harpsichord arpeggios
    $: note("c3 e3 g3 c4 g3 e3".fast(2))
    .s("triangle")
    .lpf(3000)
    .decay(0.1)
    .sustain(0.1)
    .release(0.2)
    .gain(0.25)
    .room(0.5)
    .pan(sine.range(0.3, 0.7).slow(4))
    ```
    [Listen on Strudel](https://strudel.cc/#c2V0Y3BtKDEwOC80KQoKbGV0IGNob3JkcyA9IGNob3JkKGA8QyBBbSBEbSBHNyBDIEYgRzcgQyBBbSBEbSBHNyBDIEYgRG0gRzcgQz5gKQoKLy8gc3RyaW5ncyBwYWQKJDogY2hvcmRzLm1vZGUoImJlbG93OmM1Iikudm9pY2luZygpCiAgLnNvdW5kKCJnbV9zeW50aF9zdHJpbmdzXzEiKS5nYWluKDAuMjIpCiAgLnJvb20oMC42KS5zaXplKDAuODUpLnJlbGVhc2UoMS4yKQoKLy8gbGVmdC1oYW5kIEFsYmVydGkgYmFzcyAocGlhbm8pCiQ6IG4oIjAgMiAxIDIiKS5mYXN0KDIpCiAgLnNldChjaG9yZHMpLm1vZGUoInJvb3Q6YzIiKS52b2ljaW5nKCkKICAuc291bmQoInBpYW5vIikuZ2FpbigwLjU1KS5jbGlwKDAuOSkKCi8vIHJpZ2h0LWhhbmQgbWVsb2R5IChwaWFubykKbGV0IG1lbG9keSA9IG4oYDxbMiA0IDUgNF0gWzUgNCAzIDRdIFsxIDIgMyA0XSBbNCAzIDIgNF0KWzUgNiA3IDZdIFszIDQgNSA0XSBbMiAzIDQgM10gWzIgMSAwQDIgLV0KWzUgNyA2IDVdIFsxIDMgMiAxXSBbNCAzIDIgMV0gWzAgMiA0IDJdClszIDUgNCAzXSBbMiAxIDAgMV0gWzQgNiA1IDRdIFsyIDEgMEAzIC1dPmApCiQ6IG1lbG9keS5zY2FsZSgiQzU6bWFqb3IiKQogIC5zb3VuZCgicGlhbm8iKS5nYWluKDAuODUpLmNsaXAoMS4xKQogIC5yb29tKDAuMzUpLnNpemUoMC42NSk%3D)
    </details>

    <details markdown="1">
    <summary>Opus 4.5 High Thinking produced 1-shot response, short, but sounds nicer than the first piece. The chord is dead code and never executes.</summary>
    ```javascript
    // "Moonlit Minuet" - Classical Waltz
    setcps(0.4)

    // Chord progression (strings ensemble)
    $: chord("<C4 E4 G4> <G3 B3 D4> <A3 C4 E4> <F3 A3 C4>")
    .voicing()
    .s("sawtooth")
    .lpf(1500)
    .decay(0.5)
    .sustain(0.4)
    .release(0.6)
    .gain(0.3)
    .room(0.5)
    .slow(2)

    // Melody line
    $: note("g4 a4 b4 c5 d5 c5 b4 a4 g4 ~ ~ ~")
    .s("sine")
    .lpf(4000)
    .decay(0.2)
    .sustain(0.5)
    .release(0.4)
    .gain(0.4)
    .room(0.4)
    .delay(0.15)

    // Walking bass
    $: note("c2 e2 g2 e2 g2 b2 d3 b2 a2 c3 e3 c3 f2 a2 c3 a2")
    .s("sawtooth")
    .lpf(600)
    .decay(0.3)
    .sustain(0.5)
    .gain(0.45)
    .room(0.3)
    .slow(2)

    // Ornamental trills
    $: note("g5 a5 g5 ~ ~ ~ b5 c6 b5 ~ ~ ~")
    .s("triangle")
    .lpf(5000)
    .decay(0.05)
    .sustain(0.1)
    .release(0.15)
    .gain(0.2)
    .room(0.6)
    .fast(2)
    ```
    [Listen on Strudel](https://strudel.cc/#Ly8gIk1vb25saXQgTWludWV0IiAtIENsYXNzaWNhbCBXYWx0egpzZXRjcHMoMC40KQoKLy8gQ2hvcmQgcHJvZ3Jlc3Npb24gKHN0cmluZ3MgZW5zZW1ibGUpCiQ6IGNob3JkKCI8QzQgRTQgRzQ%2BIDxHMyBCMyBEND4gPEEzIEM0IEU0PiA8RjMgQTMgQzQ%2BIikKICAudm9pY2luZygpCiAgLnMoInNhd3Rvb3RoIikKICAubHBmKDE1MDApCiAgLmRlY2F5KDAuNSkKICAuc3VzdGFpbigwLjQpCiAgLnJlbGVhc2UoMC42KQogIC5nYWluKDAuMykKICAucm9vbSgwLjUpCiAgLnNsb3coMikKCi8vIE1lbG9keSBsaW5lCiQ6IG5vdGUoImc0IGE0IGI0IGM1IGQ1IGM1IGI0IGE0IGc0IH4gfiB%2BIikKICAucygic2luZSIpCiAgLmxwZig0MDAwKQogIC5kZWNhYygwLjIpCiAgLnN1c3RhaW4oMC41KQogIC5yZWxlYXNlKDAuNCkKICAuZ2FpbigwLjQpCiAgLnJvb20oMC40KQogIC5kZWxheSgwLjE1KQoKLy8gV2Fsa2luZyBiYXNzCiQ6IG5vdGUoImMyIGUyIGcyIGUyIGcyIGIyIGQzIGIyIGEyIGMzIGUzIGMzIGYyIGEyIGMzIGEyIikKICAucygic2F3dG9vdGgiKQogIC5scGYoNjAwKQogIC5kZWNhYygwLjMpCiAgLnN1c3RhaW4oMC41KQogIC5nYWluKDAuNDUpCiAgLnJvb20oMC4zKQogIC5zbG93KDIpCgovLyBPcm5hbWVudGFsIHRyaWxscwokOiBub3RlKCJnNSBhNSBnNSB%2BIH4gfiBiNSBjNiBiNSB%2BIH4gfiIpCiAgLnMoInRyaWFuZ2xlIikKICAubHBmKDUwMDApCiAgLmRlY2F5KDAuMDUpCiAgLnN1c3RhaW4oMC4xKQogIC5yZWxlYXNlKDAuMTUpCiAgLmdhaW4oMC4yKQogIC5yb29tKDAuNikKICAuZmFzdCgyKQ%3D%3D)
    </details>

    <details markdown="1">
    <summary>Sonnet 4.5 Thinking created 1-shot short composition that sounded suspiciously familiar.</summary>
    ```javascript
    // Classical Piano Piece in Strudel
    // Inspired by baroque/classical counterpoint

    stack(
    // Main melody (right hand) - inspired by Bach-style invention
    note("c5 d5 e5 f5 g5 f5 e5 d5")
        .s("piano")
        .velocity(0.7)
        .slow(2),
    
    // Counter melody (left hand)
    note("c3 g3 e3 g3 c3 g3 e3 g3")
        .s("piano")
        .velocity(0.5)
        .slow(2),
    
    // Bass line
    note("c2 c2 g2 g2")
        .s("piano")
        .velocity(0.6)
        .slow(4)
    ).slow(1.5)
    ```
    [Listen on Strudel](https://strudel.cc/#Ly8gQ2xhc3NpY2FsIFBpYW5vIFBpZWNlIGluIFN0cnVkZWwKLy8gSW5zcGlyZWQgYnkgYmFyb3F1ZS9jbGFzc2ljYWwgY291bnRlcnBvaW50CgpzdGFjaygKICAvLyBNYWluIG1lbG9keSAocmlnaHQgaGFuZCkgLSBpbnNwaXJlZCBieSBCYWNoLXN0eWxlIGludmVudGlvbgogIG5vdGUoImM1IGQ1IGU1IGY1IGc1IGY1IGU1IGQ1IikKICAgIC5zKCJwaWFubyIpCiAgICAudmVsb2NpdHkoMC43KQogICAgLnNsb3coMiksCiAgCiAgLy8gQ291bnRlciBtZWxvZHkgKGxlZnQgaGFuZCkKICBub3RlKCJjMyBnMyBlMyBnMyBjMyBnMyBlMyBnMyIpCiAgICAucygicGlhbm8iKQogICAgLnZlbG9jaXR5KDAuNSkKICAgIC5zbG93KDIpLAogIAogIC8vIEJhc3MgbGluZQogIG5vdGUoImMyIGMyIGcyIGcyIikKICAgIC5zKCJwaWFubyIpCiAgICAudmVsb2NpdHkoMC42KQogICAgLnNsb3coNCkKKS5zbG93KDEuNSk%3D)
    </details>

    <details markdown="1">
    <summary>Sonnet 4.5 Thinking created 1-shot composition that was absolutely silent, but executing code.</summary>
    ```javascript
    // Classical String Quartet Style
    stack(
    // Violin I - main theme
    note("<[c5 e5 g5 c6] [b4 d5 g5 b5]>")
        .s("violin")
        .velocity(0.8),
    
    // Violin II - harmony
    note("<[e4 g4 c5 e5] [d4 g4 b4 d5]>")
        .s("violin")
        .velocity(0.6),
    
    // Viola - inner voice
    note("<[g3 c4 e4 g4] [g3 b3 d4 g4]>")
        .s("viola")
        .velocity(0.5),
    
    // Cello - bass
    note("<c3 g3>")
        .s("cello")
        .velocity(0.7)
        .slow(2)
    )
    ```
    [Listen on Strudel](https://strudel.cc/#Ly8gQ2xhc3NpY2FsIFN0cmluZyBRdWFydGV0IFN0eWxlCnN0YWNrKAogIC8vIFZpb2xpbiBJIC0gbWFpbiB0aGVtZQogIG5vdGUoIjxbYzUgZTUgZzUgYzZdIFtiNCBkNSBnNSBiNV0%2BIikKICAgIC5zKCJ2aW9saW4iKQogICAgLnZlbG9jaXR5KDAuOCksCiAgCiAgLy8gVmlvbGluIElJIC0gaGFybW9ueQogIG5vdGUoIjxbZTQgZzQgYzUgZTVdIFtkNCBnNCBiNCBkNV0%2BIikKICAgIC5zKCJ2aW9saW4iKQogICAgLnZlbG9jaXR5KDAuNiksCiAgCiAgLy8gVmlvbGEgLSBpbm5lciB2b2ljZQogIG5vdGUoIjxbZzMgYzQgZTQgZzRdIFtnMyBiMyBkNCBnNF0%2BIikKICAgIC5zKCJ2aW9sYSIpCiAgICAudmVsb2NpdHkoMC41KSwKICAKICAvLyBDZWxsbyAtIGJhc3MKICBub3RlKCI8YzMgZzM%2BIikKICAgIC5zKCJjZWxsbyIpCiAgICAudmVsb2NpdHkoMC43KQogICAgLnNsb3coMikKKQ%3D%3D)
    </details>

*   **OpenAI:** GPT-5.2 and GPT-5.2 Codex both managed to 1-shot the more complicated lengthier compositions of this experiment. They were both the runaway winners.

    <details markdown="1">
    <summary>GPT-5.2 XHigh a complex and longer composition done in 1-shot</summary>

    ```javascript
    setcpm(108/4)

    let chords = chord(`<C Am Dm G7 C F G7 C Am Dm G7 C F Dm G7 C>`)

    // strings pad
    $: chords.mode("below:c5").voicing()
    .sound("gm_synth_strings_1").gain(0.22)
    .room(0.6).size(0.85).release(1.2)

    // left-hand Alberti bass (piano)
    $: n("0 2 1 2").fast(2)
    .set(chords).mode("root:c2").voicing()
    .sound("piano").gain(0.55).clip(0.9)

    // right-hand melody (piano)
    let melody = n(`<[2 4 5 4] [5 4 3 4] [1 2 3 4] [4 3 2 4]
    [5 6 7 6] [3 4 5 4] [2 3 4 3] [2 1 0@2 -]
    [5 7 6 5] [1 3 2 1] [4 3 2 1] [0 2 4 2]
    [3 5 4 3] [2 1 0 1] [4 6 5 4] [2 1 0@3 -]>`)
    $: melody.scale("C5:major")
    .sound("piano").gain(0.85).clip(1.1)
    .room(0.35).size(0.65)
    ```
    [Listen on Strudel](https://strudel.cc/#c2V0Y3BtKDEwOC80KQoKbGV0IGNob3JkcyA9IGNob3JkKGA8QyBBbSBEbSBHNyBDIEYgRzcgQyBBbSBEbSBHNyBDIEYgRG0gRzcgQz5gKQoKLy8gc3RyaW5ncyBwYWQKJDogY2hvcmRzLm1vZGUoImJlbG93OmM1Iikudm9pY2luZygpCiAgLnNvdW5kKCJnbV9zeW50aF9zdHJpbmdzXzEiKS5nYWluKDAuMjIpCiAgLnJvb20oMC42KS5zaXplKDAuODUpLnJlbGVhc2UoMS4yKQoKLy8gbGVmdC1oYW5kIEFsYmVydGkgYmFzcyAocGlhbm8pCiQ6IG4oIjAgMiAxIDIiKS5mYXN0KDIpCiAgLnNldChjaG9yZHMpLm1vZGUoInJvb3Q6YzIiKS52b2ljaW5nKCkKICAuc291bmQoInBpYW5vIikuZ2FpbigwLjU1KS5jbGlwKDAuOSkKCi8vIHJpZ2h0LWhhbmQgbWVsb2R5IChwaWFubykKbGV0IG1lbG9keSA9IG4oYDxbMiA0IDUgNF0gWzUgNCAzIDRdIFsxIDIgMyA0XSBbNCAzIDIgNF0KWzUgNiA3IDZdIFszIDQgNSA0XSBbMiAzIDQgM10gWzIgMSAwQDIgLV0KWzUgNyA2IDVdIFsxIDMgMiAxXSBbNCAzIDIgMV0gWzAgMiA0IDJdClszIDUgNCAzXSBbMiAxIDAgMV0gWzQgNiA1IDRdIFsyIDEgMEAzIC1dPmApCiQ6IG1lbG9keS5zY2FsZSgiQzU6bWFqb3IiKQogIC5zb3VuZCgicGlhbm8iKS5nYWluKDAuODUpLmNsaXAoMS4xKQogIC5yb29tKDAuMzUpLnNpemUoMC42NSk%3D)
    </details>

    <details markdown="1">
    <summary>GPT-5.2 Codex XHigh a complex and longer composition done in 1-shot that would feel at home as a video game midi background track.</summary>

    ```javascript
    setcpm(96/3)

    const melody = cat(
    "e5 d5 c5 d5 e5 g5",
    "d5 e5 f5 g5 a5 g5",
    "e5 c5 a4 c5 e5 g5",
    "f5 e5 d5 c5 d5 b4",
    "c5 d5 e5 f5 g5 f5",
    "e5 d5 c5 e5 g5 e5",
    "d5 b4 g4 b4 d5 f5",
    "e5 d5 c5 g4 c5 ~"
    ).note().s("sine").gain(0.7)

    const chords = cat(
    "~ [c4,e4,g4] [c4,e4,g4]",
    "~ [g3,b3,d4] [g3,b3,d4]",
    "~ [a3,c4,e4] [a3,c4,e4]",
    "~ [g3,b3,d4] [g3,b3,d4]",
    "~ [f3,a3,c4] [f3,a3,c4]",
    "~ [c4,e4,g4] [c4,e4,g4]",
    "~ [g3,b3,d4] [g3,b3,d4]",
    "~ [c4,e4,g4] [c4,e4,g4]"
    ).note().s("triangle").gain(0.5)

    const bass = cat(
    "c2 ~ g1",
    "g2 ~ d2",
    "a2 ~ e2",
    "g2 ~ d2",
    "f2 ~ c2",
    "c2 ~ g1",
    "g2 ~ d2",
    "c2 ~ g1"
    ).note().s("sawtooth").gain(0.6).cutoff(800)

    stack(melody, chords, bass)
    ```
    [Listen on Strudel](https://strudel.cc/#c2V0Y3BtKDk2LzMpCgpjb25zdCBtZWxvZHkgPSBjYXQoCiAgImU1IGQ1IGM1IGQ1IGU1IGc1IiwKICAiZDUgZTUgZjUgZzUgYTUgZzUiLAogICJlNSBjNSBhNCBjNSBlNSBnNSIsCiAgImY1IGU1IGQ1IGM1IGQ1IGI0IiwKICAiYzUgZDUgZTUgZjUgZzUgZjUiLAogICJlNSBkNSBjNSBlNSBnNSBlNSIsCiAgImQ1IGI0IGc0IGI0IGQ1IGY1IiwKICAiZTUgZDUgYzUgZzQgYzUgfiIKKS5ub3RlKCkucygic2luZSIpLmdhaW4oMC43KQoKY29uc3QgY2hvcmRzID0gY2F0KAogICJ%2BIFtjNCxlNCxnNF0gW2M0LGU0LGc0XSIsCiAgIn4gW2czLGIzLGQ0XSBbZzMsYjMsZDRdIiwKICAifiBbYTMsYzQsZTRdIFthMyxjNCxlNF0iLAogICJ%2BIFtnMyxiMyxkNF0gW2czLGIzLGQ0XSIsCiAgIn4gW2YzLGEzLGM0XSBbZjMsYTMsYzRdIiwKICAifiBbYzQsZTQsZzRdIFtjNCxlNCxnNF0iLAogICJ%2BIFtnMyxiMyxkNF0gW2czLGIzLGQ0XSIsCiAgIn4gW2M0LGU0LGc0XSBbYzQsZTQsZzRdIgopLm5vdGUoKS5zKCJ0cmlhbmdsZSIpLmdhaW4oMC41KQoKY29uc3QgYmFzcyA9IGNhdCgKICAiYzIgfiBnMSIsCiAgImcyIH4gZDIiLAogICJhMiB%2BIGUyIiwKICAiZzIgfiBkMiIsCiAgImYyIH4gYzIiLAogICJjMiB%2BIGcxIiwKICAiZzIgfiBkMiIsCiAgImMyIH4gZzEiCikubm90ZSgpLnMoInNhd3Rvb3RoIikuZ2FpbigwLjYpLmN1dG9mZig4MDApCgpzdGFjayhtZWxvZHksIGNob3JkcywgYmFzcyk%3D)
    </details>

*   **xAI Grok:** Each of the tested grok models managed to generate a composition, though the results were too noisy and chaotic.

    <details markdown="1">
    <summary>Grok 4.1 Thinking created this loud composition in 1-shot, it feels like it could be a part of a much larger professional piece.</summary>

    ```javascript
    setcps(0.6)

    stack(
    // Ground bass (slow, sustained roots)
    note("<d2 a2 b2 fis2 g2 d2 g2 a2>").slow(2).s("piano").legato(1).gain(1.2),

    // Layered arpeggios (staggered for richness, changing per chord)
    stack(
        note("<d4 fs4 a4 d5> <e4 a4 cs5 e5> <fs4 b4 d5 fs5> <fis4 a4 cs5 fis5> <g4 b4 d5 g5> <fs4 a4 d5 fs5> <g4 b4 d5 g5> <a4 cs5 e5 a5>").fast(8),
        note("<fs4 a4 d5 fs5> <a4 cs5 e5 a5> <b4 d5 fs5 b5> <a4 cs5 fis5 a5> <b4 d5 g5 b5> <a4 d5 fs5 a5> <b4 d5 g5 b5> <cs5 e5 a5 cs6>").fast(8).late(0.125),
        note("<a4 d5 fs5 a5> <cs5 e5 a5 cs6> <d5 fs5 b5 d6> <cs5 fis5 a5 cs6> <d5 g5 b5 d6> <d5 fs5 a5 d6> <d5 g5 b5 d6> <e5 a5 cs6 e6>").fast(8).late(0.25)
    ).s("piano").gain(0.7),

    // Canonic melody entries (violin-like lines entering sequentially)
    note("a5 fs5 d5 fs5 e5 cs5 d5 b4 cs5 a4 b4 g4 a4 fs4 g4 e4").s("piano").gain(0.9).late(8),
    note("a5 fs5 d5 fs5 e5 cs5 d5 b4 cs5 a4 b4 g4 a4 fs4 g4 e4").s("piano").gain(0.9).late(16),
    note("a5 fs5 d5 fs5 e5 cs5 d5 b4 cs5 a4 b4 g4 a4 fs4 g4 e4").s("piano").gain(0.9).late(24)
    ).room(0.8).delay(0.4)
    ```
    [Listen on Strudel](https://strudel.cc/#c2V0Y3BzKDAuNikKCnN0YWNrKAogIC8vIEdyb3VuZCBib3NzIChzbG93LCBzdXN0YWluZWQgcm9vdHMpCiAgbm90ZSgiPGQyIGEyIGIyIGZpczIgZzIgZDIgZzIgYTI%2BIikuc2xvdygyKS5zKCJwaWFubyIpLmxlZ2F0bygxKS5nYWluKDEuMiksCgogIC8vIExheWVyZWQgYXJwZWdnaW9zIChzdGFnZ2VyZWQgZm9yIHJpY2huZXNzLCBjaGFuZ2luZyBwZXIgY2hvcmQpCiAgc3RhY2soCiAgICBub3RlKCI8ZDQgZnM0IGE0IGQ1PiA8ZTQgYTQgY3M1IGU1PiA8ZnM0IGI0IGQ1IGZzNT4gPGZpczQgYTQgY3M1IGZpczU%2BIDxnNCBiNCBkNSBnNT4gPGZzNCBhNCBkNSBmczU%2BIDxnNCBiNCBkNSBnNT4gPGE0IGNzNSBlNSBhNT4iKS5mYXN0KDgpLAog샨bm90ZSgiPGZzNCBhNCBkNSBmczU%2BIDxhNCBjczUgZTUgYTU%2BIDxiNCBkNSBmczUgYjU%2BIDxhNCBjczUgZmlzNSBhNT4gPGI0IGQ1IGc1IGI1PiA8YTQgZDUgZnM1IGE1PiA8YjQgZDUgZzUgYjU%2BIDxjczUgZTUgYTUgY3M2PiIpLmZhc3QoOCkubGF0ZSgwLjEyNSksCiAgICBub3RlKCI8YTQgZDUgZnM1IGE1PiA8Y3M1IGU1IGE1IGNzNj4gPGQ1IGZzNSBiNSBkNj4gPGNzNSBmaXM1IGE1IGNzNj4gPGQ1IGc1IGI1IGQ2PiA8ZDUgZnM1IGE1IGQ2PiA8ZDUgZzUgYjUgZDY%2BIDxlNSBhNSBjczYgZTY%2BIikuZmFzdCg4KS5sYXRlKDAuMjUpCiAgKS5zKCJwaWFubyIpLmdhaW4oMC43KSwKCiAgLy8gQ2Fub25pYyBtZWxvZHkgZW50cmllcyAodmlvbGluLWxpa2UgbGluZXMgZW50ZXJpbmcgc2VxdWVudGlhbGx5KQogIG5vdGUoImE1IGZzNSBkNSBmczUgZTUgY3M1IGQ1IGI0IGNzNSBhNCBiNCBnNCBhNCBmczQgZzQgZTQiKS5zKCJwaWFubyIpLmdhaW4oMC45KS5sYXRlKDgpLAogIG5vdGUoImE1IGZzNSBkNSBmczUgZTUgY3M1IGQ1IGI0IGNzNSBhNCBiNCBnNCBhNCBmczQgZzQgZTQiKS5zKCJwaWFubyIpLmdhaW4oMC45KS5sYXRlKDE2KSwKICBub3RlKCJhNSBmczUgZDUgZnM1IGU1IGNzNSBkNSBiNCBjczUgYTQgYjQgZzQgYTQgZnM0IGc0IGU0IikucygicGlhbm8iKS5nYWluKDAuOSkubGF0ZSgyNCkKKS5yb29tKDAuOCkuZGVsYXkoMC40KQ%3D%3D)
    </details>

    <details markdown="1">
    <summary>Grok code fast 1 managed to 1-shot this unlistenable noisy composition that crashes strudel for me if I play it too long.</summary>

    ```javascript
    // Classical Composition: Baroque-Inspired Fugue
    // Theme in D minor
    const theme = "d3 a3 f3 d3 c4 a3 f3 d3"

    // Countersubject
    const countersubject = "f3 g3 a3 bes3 c4 d4 ees4 f4"

    // Main fugue structure
    stack(
    // Subject entries at different intervals
    n(theme).s("piano").delay(0),
    n(theme).s("piano").delay(4).transpose(5), // Dominant
    n(theme).s("piano").delay(8).transpose(-2), // Subdominant
    
    // Countersubject
    n(countersubject).s("strings").delay(2),
    n(countersubject).s("strings").delay(6).transpose(5),
    
    // Bass line (walking bass in D minor)
    n("d2 f2 a2 d2 c3 a2 f2 d2").s("cello").delay(0),
    
    // Harmonic progression
    chord("Dm Gm Am Dm Bb F C Gm").s("organ").delay(0).gain(0.3),
    
    // Ornamentation and flourishes
    n("d4 f4 a4 d5").s("flute").delay(12).euclid(3,8),
    n("a3 c4 e4 a4").s("violin").delay(14).euclid(5,8)
    ).fast(1/2)
    ```
    [Listen on Strudel](https://strudel.cc/#Ly8gQ2xhc3NpY2FsIENvbXBvc2l0aW9uOiBCYXJvcXVlLUluc3BpcmVkIEZ1Z3VlCi8vIFRoZW1lIGluIEQgbWlub3IKY29uc3QgdGhlbWUgPSAiZDMgYTMgZjMgZDMgYzQgYTMgZjMgZDMiCgovLyBDb3VudGVyc3ViamVjdApjb25zdCBjb3VudGVyc3ViamVjdCA9ICJmMyBnMyBhMyBiZXMzIGM0IGQ0IGVlczQgZjQiCgovLyBNYWluIGZ1Z3VlIHN0cnVjdHVyZQpzdGFjaygKICAvLyBTdWJqZWN0IGVudHJpZXMgYXQgZGlmZmVyZW50IGludGVydmFscwogIG4odGhlbWUpLnMoInBpYW5vIikuZGVsYXkoMCksCiAgbih0aGVtZSkucygicGlhbm8iKS5kZWxheSg0KS50cmFuc3Bvc2UoNSksIC8vIERvbWluYW50CiAgbih0aGVtZSkucygicGlhbm8iKS5kZWxheSg4KS50cmFuc3Bvc2UoLTIpLCAvLyBTdWJkb21pbmFudAogIAogIC8vIENvdW50ZXJzdWJqZWN0CiAgbihjb3VudGVyc3ViamVjdCkucygic3RyaW5ncyIpLmRlbGF5KDIpLAogIG4oY291bnRlcnN1YmplY3QpLnMoInN0cmluZ3MiKS5kZWxheSg2KS50cmFuc3Bvc2UoNSksCiAgCiAgLy8gQmFzcyBsaW5lICh3YWxraW5nIGJhc3MgaW4gRCBtaW5vcikKICBuKCJkMiBmMiBhMiBkMiBjMyBhMiBmMiBkMiIpLnMoImNlbGxvIikuZGVsYXkoMCksCiAgCiAgLy8gSGFybW9uaWMgcHJvZ3Jlc3Npb24KICBjaG9yZCgiRG0gR20gQW0gRG0gQmIgRiBDIEdtIikucyib3JnYW4iKS5kZWxheSgwKS5nYWluKDAuMyksCiAgCiAgLy8gT3JuYW1lbnRhdGlvbiBhbmQgZmxvdXJpc2hlcwogIG4oImQ0IGY0IGE0IGQ1IikucygiZmx1dGUiKS5kZWxheSgxMikuZXVjbGlkKDMsOCksCiAgbigiYTMgYzQgZTQgYTQiKS5zKCJ2aW9saW4iKS5kZWxheSgxNCkuZXVjbGlkKDUsOCkKKS5mYXN0KDEvMik%3D)
    </details>

*   **The Epilogue:** Claude Opus 4.6 and GPT 5.3 Codex were both recently released on February 5th, 2026.

    <details markdown="1">
    <summary>Opus 4.6 High Thinking was a noticeably upgrade where it now 1-shot compositions like GPT 5.2 or GPT 5.2 Codex did.</summary>

    ```javascript
    // "Reverie in D minor" — A Classical Composition for Strudel
    // Inspired by Baroque counterpoint and Classical-era harmony

    setcps(0.48)

    // Soprano melody — lyrical, singing line
    let soprano = note(
    `<[d5 e5 f5 g5] [a5 ~ g5 f5] [e5 f5 g5 a5] [f5 ~ e5 d5]
    [c#5 d5 e5 f5] [g5 ~ f5 e5] [f5 e5 d5 c#5] [d5 ~ ~ ~]
    [a4 bb4 c5 d5] [e5 f5 g5 f5] [e5 d5 c5 bb4] [a4 ~ g4 a4]
    [bb4 c5 d5 e5] [f5 e5 d5 c#5] [d5 e5 f5 e5] [d5 ~ ~ ~]>`
    )
    .s("triangle")
    .lpf(sine.range(1500, 3500).slow(16))
    .attack(0.01).decay(0.25).sustain(0.55).release(0.5)
    .gain(0.5)
    .room(0.5).size(0.7)
    .delay(0.12).delaytime(0.375).delayfeedback(0.2)

    // Alto — gentle inner voice providing harmonic color
    let alto = note(
    `<[a4 ~ a4 ~] [f4 ~ e4 ~] [c4 ~ e4 ~] [d4 ~ ~ ~]
    [e4 ~ e4 ~] [e4 ~ c#4 ~] [d4 ~ a3 ~] [a4 ~ ~ ~]
    [f4 ~ f4 ~] [g4 ~ a4 ~] [g4 ~ e4 ~] [f4 ~ e4 ~]
    [d4 ~ e4 ~] [a4 ~ a4 ~] [a4 ~ a4 ~] [f4 ~ ~ ~]>`
    )
    .s("triangle")
    .lpf(1600)
    .attack(0.05).decay(0.3).sustain(0.4).release(0.6)
    .gain(0.28)
    .room(0.5).size(0.6)

    // Bass — stately, cello-like foundation
    let bass = note(
    `<[d3 ~ a2 ~] [d3 ~ c3 ~] [c3 ~ c3 ~] [d3 ~ d3 ~]
    [a2 ~ a2 ~] [bb2 ~ a2 ~] [d3 ~ a2 ~] [d3 ~ ~ ~]
    [f2 ~ f2 ~] [c3 ~ c3 ~] [c3 ~ c3 ~] [f2 ~ c3 ~]
    [bb2 ~ bb2 ~] [a2 ~ a2 ~] [d3 ~ a2 ~] [d3 ~ ~ ~]>`
    )
    .s("sawtooth")
    .lpf(700)
    .attack(0.02).decay(0.35).sustain(0.65).release(0.6)
    .gain(0.42)
    .room(0.4).size(0.5)

    // Sustained chords — organ-like pads for warmth
    let chords = note(
    `<[d4,f4,a4] [d4,f4,a4] [c4,e4,a4] [d4,f4,a4]
    [c#4,e4,a4] [bb3,d4,g4] [a3,d4,f4] [a3,d4,f4]
    [c4,f4,a4] [c4,e4,g4] [c4,e4,g4] [c4,f4,a4]
    [bb3,d4,f4] [a3,c#4,e4] [a3,d4,f4] [a3,d4,f4]>`
    )
    .s("triangle")
    .lpf(1200)
    .attack(0.15).decay(0.5).sustain(0.5).release(1.0)
    .gain(0.18)
    .room(0.7).size(0.8)
    .slow(2)

    stack(soprano, alto, bass, chords)
    ```
    [Listen on Strudel](https://strudel.cc/#Ly8gIlJldmVyaWUgaW4gRCBtaW5vciIg4oCUIEEgQ2xhc3NpY2FsIENvbXBvc2l0aW9uIGZvciBTdHJ1ZGVsCi8vIEluc3BpcmVkIGJ5IEJhcm9xdWUgY291bnRlcnBvaW50IGFuZCBDbGFzc2ljYWwtZXJhIGhhcm1vbnkKCnNldGNwcygwLjQ4KQoKLy8gU29wcmFubyBtZWxvZHkg4oCUIGx5cmljYWwsIHNpbmdpbmcgbGluZQpsZXQgc29wcmFubyA9IG5vdGUoCiAgYDxbZDUgZTUgZjUgZzVdIFthNSB%2BIGc1IGY1XSBbZTUgZjUgZzUgYTVdIFtmNSB%2BIGU1IGQ1XQogICBbYyM1IGQ1IGU1IGY1XSBbZzUgfiBmNSBlNV0gW2Y1IGU1IGQ1IGMjNV0gW2Q1IH4gfiB%2BXQogICBbYTQgYmI0IGM1IGQ1XSBbZTUgZjUgZzUgZjVdIFtlNSBkNSBjNSBiYjRdIFthNCB%2BIGc0IGE0XQogICBbYmI0IGM1IGQ1IGU1XSBbZjUgZTUgZDUgYyM1XSBbZDUgZTUgZjUgZTVdIFtkNSB%2BIH4gfl0%2BYAopCiAgLnMoInRyaWFuZ2xlIikKICAubHBmKHNpbmUucmFuZ2UoMTUwMCwgMzUwMCkuc2xvdygxNikpCiAgLmF0dGFjaygwLjAxKS5kZWNheSgwLjI1KS5zdXN0YWluKDAuNTUpLnJlbGVhc2UoMC41KQogIC5nYWluKDAuNSkKICAucm9vbSgwLjUpLnNpemUoMC43KQogIC5kZWxheSgwLjEyKS5kZWxheXRpbWUoMC4zNzUpLmRlbGF5ZmVlZGJhY2soMC4yKQoKLy8gQWx0byDigJQgZ2VudGxlIGlubmVyIHZvaWNlIHByb3ZpZGluZyBoYXJtb25pYyBjb2xvcgpsZXQgYWx0byA9IG5vdGUoCiAgYDxbYTQgfiBhNCB%2BXSBbZjQgfiBlNCB%2BXSBbYzQgfiBlNCB%2BXSBbZDQgfiB%2BIH5dCiAgIFtlNCB%2BIGU0IH5dIFtlNCB%2BIGMjNCB%2BXSBbZDQgfiBhMyB%2BXSBbYTQgfiB%2BIH5dCiAgIFtmNCB%2BIGY0IH5dIFtnNCB%2BIGE0IH5dIFtnNCB%2BIGU0IH5dIFtmNCB%2BIGU0IH5dCiAgIFtkNCB%2BIGU0IH5dIFthNCB%2BIGE0IH5dIFthNCB%2BIGE0IH5dIFtmNCB%2BIH4gfl0%2BYAopCiAgLnMoInRyaWFuZ2xlIikKICAubHBmKDE2MDApCiAgLmF0dGFjaygwLjA1KS5kZWNheSgwLjMpLnN1c3RhaW4oMC40KS5yZWxlYXNlKDAuNikKICAuZ2FpbigwLjI4KQogIC5yb29tKDAuNSkuc2l6ZSgwLjYpCgovLyBCYXNzIOKAlCBzdGF0ZWx5LCBjZWxsby1saWtlIGZvdW5kYXRpb24KbGV0IGJhc3MgPSBub3RlKAogIGA8W2QzIH4gYTIgfl0gW2QzIH4gYzMgfl0gW2MzIH4gYzMgfl0gW2QzIH4gZDMgfl0KICAgW2EyIH4gYTIgfl0gW2JiMiB%2BIGEyIH5dIFtkMyB%2BIGEyIH5dIFtkMyB%2BIH4gfl0KICAgW2YyIH4gZjIgfl0gW2MzIH4gYzMgfl0gW2MzIH4gYzMgfl0gW2YyIH4gYzMgfl0KICAgW2JiMiB%2BIGJiMiB%2BXSBbYTIgfiBhMiB%2BXSBbZDMgfiBhMiB%2BXSBbZDMgfiB%2BIH5dPmAKKQogIC5zKCJzYXd0b290aCIpCiAgLmxwZig3MDApCiAgLmF0dGFjaygwLjAyKS5kZWNheSgwLjM1KS5zdXN0YWluKDAuNjUpLnJlbGVhc2UoMC42KQogIC5nYWluKDAuNDIpCiAgLnJvb20oMC40KS5zaXplKDAuNSkKCi8vIFN1c3RhaW5lZCBjaG9yZHMg4oCUIG9yZ2FuLWxpa2UgcGFkcyBmb3Igd2FybXRoCmxldCBjaG9yZHMgPSBub3RlKAogIGA8W2Q0LGY0LGE0XSBbZDQsZjQsYTRdIFtjNCxlNCxhNF0gW2Q0LGY0LGE0XQogICBbYyM0LGU0LGE0XSBbYmIzLGQ0LGc0XSBbYTMsZDQsZjRdIFthMyxkNCxmNF0KICAgW2M0LGY0LGE0XSBbYzQsZTQsZzRdIFtjNCxlNCxnNF0gW2M0LGY0LGE0XQogICBbYmIzLGQ0LGY0XSBbYTMsYyM0LGU0XSBbYTMsZDQsZjRdIFthMyxkNCxmNF0%2BYAopCiAgLnMoInRyaWFuZ2xlIikKICAubHBmKDEyMDApCiAgLmF0dGFjaygwLjE1KS5kZWNheSgwLjUpLnN1c3RhaW4oMC41KS5yZWxlYXNlKDEuMCkKICAuZ2FpbigwLjE4KQogIC5yb29tKDAuNykuc2l6ZSgwLjgpCiAgLnNsb3coMikKCnN0YWNrKHNvcHJhbm8sIGFsdG8sIGJhc3MsIGNob3Jkcyk%3D)
    </details>

    <details markdown="1">
    <summary>Codex 5.3 XHigh is still the king of strudel music generation with a noticeable improvement over its 5.2 models.</summary>

    ```javascript
    setcpm(72)

    const harmony = "<[c4 e4 g4] [a3 c4 e4] [d4 f4 a4] [g3 b3 d4] [c4 e4 g4] [f3 a3 c4] [d4 f4 a4] [g3 b3 d4]>"
    const bassline = "<c2 a1 d2 g1 c2 f1 d2 g1>"
    const melody = "<e5 g5 a5 g5 e5 d5 c5 b4 c5 d5 e5 g5 f5 e5 d5 c5>"
    const strings = "<g4 a4 b4 c5 b4 a4 g4 f4>"

    stack(
    note(harmony)
        .slow(2)
        .sound("gm_acoustic_grand_piano")
        .gain(0.58)
        .release(1.25)
        .room(0.24)
        .size(0.72),

    note(bassline)
        .slow(2)
        .sound("gm_acoustic_bass")
        .gain(0.52)
        .release(0.9)
        .lpf(900),

    note(melody)
        .slow(2)
        .sound("gm_violin")
        .legato(1.08)
        .gain(0.7)
        .room(0.34)
        .size(0.82),

    note(strings)
        .slow(4)
        .sound("gm_string_ensemble_1")
        .legato(1.2)
        .gain(0.34)
        .room(0.5)
        .size(0.95)
    )
    ```
    [Listen on Strudel](https://strudel.cc/#c2V0Y3BtKDcyKQoKY29uc3QgaGFybW9ueSA9ICI8W2M0IGU0IGc0XSBbYTMgYzQgZTRdIFtkNCBmNCBhNF0gW2czIGIzIGQ0XSBbYzQgZTQgZzRdIFtmMyBhMyBjNF0gW2Q0IGY0IGE0XSBbZzMgYjMgZDRdPiIKY29uc3QgYmFzc2xpbmUgPSAiPGMyIGExIGQyIGcxIGMyIGYxIGQyIGcxPiIKY29uc3QgbWVsb2R5ID0gIjxlNSBnNSBhNSBnNSBlNSBkNSBjNSBiNCBjNSBkNSBlNSBnNSBmNSBlNSBkNSBjNT4iCmNvbnN0IHN0cmluZ3MgPSAiPGc0IGE0IGI0IGM1IGI0IGE0IGc0IGY0PiIKCnN0YWNrKAogIG5vdGUoaGFybW9ueSkKICAgIC5zbG93KDIpCiAgICAuc291bmQoImdtX2Fjb3VzdGljX2dyYW5kX3BpYW5vIikKICAgIC5nYWluKDAuNTgpCiAgICAucmVsZWFzZSgxLjI1KQogICAgLnJvb20oMC4yNCkKICAgIC5zaXplKDAuNzIpLAoKICBub3RlKGJhc3NsaW5lKQogICAgLnNsb3coMikKICAgIC5zb3VuZCgiZ21fYWNvdXN0aWNfYmFzcyIpCiAgICAuZ2FpbigwLjUyKQogICAgLnJlbGVhc2UoMC45KQogICAgLmxwZig5MDApLAoKICBub3RlKG1lbG9keSkKICAgIC5zbG93KDIpCiAgICAuc291bmQoImdtX3Zpb2xpbiIpCiAgICAubGVnYXRvKDEuMDgpCiAgICAuZ2FpKDAuNykKICAgIC5yb29tKDAuMzQpCiAgICAuc2l6ZSgwLjgyKSwKCiAgbm90ZShzdHJpbmdzKQogICAgLnNsb3coNCkKICAgIC5zb3VuZCgiZ21fc3RyaW5nX2Vuc2VtYmxlXzEiKQogICAgLmxlZ2F0bygxLjIpCiAgICAuZ2FpKDAuMzQpCiAgICAucm9vbSgwLjUpCiAgICAuc2l6ZSgwLjk1KQoK)
    </details>

## The Paradox: Music Should Be Easy

Here's what makes these results so revealing.

Think about what we're asking these models to do. A page of music is *simpler* than a page of code. Music runs left to right — it's a linear progression. There are no function callbacks, no dependency graphs, no state management across files. A classical composition in Strudel is, structurally, a trivial task compared to the flight simulators, 3D games, and full-stack apps these same models can produce in one shot.

And LLMs should have *plenty* of music-related training data. Music theory textbooks, millions of lines of MIDI data, centuries of documented compositions. Music is one of the most well-documented human endeavors in existence.

So why do models that can scaffold an entire React app struggle to write a 30-second melody in a JavaScript DSL?

Because they haven't seen enough *Strudel-specific* examples. The issue isn't complexity — it's familiarity. When you look at the results, the pattern is unmistakable: performance correlates almost perfectly with how much Strudel-like data likely appeared in the training set. The massive frontier models (GPT-5.2, Codex) succeed because they've probably ingested more of the internet — including whatever Strudel examples exist. The smaller or more specialized models crack.

The follow-up results hammer this home. Opus 4.6 and Codex 5.3, released just weeks after the original test, showed marked improvement. Did they suddenly learn to *reason about music*? No. They got trained on more data.

## No Ghosts, Just Mirrors

I've come to a conclusion: LLMs aren't full of ghosts. They're mirrors.

They don't *understand* music or code in any sentient sense. They reflect the data we've fed them. They show us what we do the most by excelling at it. A billion Python loops in the training set? Mirrored perfectly. A handful of Strudel snippets? They crack.

They are the true successor to tab-complete — staggeringly powerful tab-complete that lets us skip the tedium and get straight to the interesting parts. But they aren't *thinking*. When Gemini fails to write Strudel despite clearly knowing the syntax exists, it's evidence that transfer learning — the hallmark of actual intelligence — is still largely missing.

The mirror is getting sharper with every generation. But it's still a mirror.

This doesn't make them useless. Far from it. It makes them the most powerful productivity tool ever created. But we should be honest about what they are: interpolation engines, not reasoning engines. Incredible at filling in patterns they've seen. Lost when they haven't.

## A Note on Safety

If the mirror thesis holds, it has uncomfortable implications for AI safety. If "dangerous" model behavior isn't emergent intelligence but just more mirroring — models reciting scripts from the dystopian novels, blackmail scenarios, and horror fiction they were trained on — then our current approach has it backwards. We spend billions on RLHF and guardrails to stop models from saying things they should never have learned in the first place.

Instead of building better cages, we should have built better diets.

## The Bottom Line

If these models were truly getting more intelligent, we would see them apply logic from one domain to another effortlessly. Instead, we see that they are only as good as their last meal of data.

We aren't witnessing an innovation in reasoning. We are witnessing an innovation in data ingestion and scale.

The intelligence is in the data, stupid.
