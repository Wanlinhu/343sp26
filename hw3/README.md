# Single Sample Song Documentation

For this assignment, I created a 1-2 minute live coding piece using only one sample: sine. I chose sine because it's my favorite sound from playing modular synthesizers — it's round, smooth, and has no harsh attack. There's something very pure about it that I find really satisfying.

## Creative Process

I started with a simple melody using the C:ritusen scale, which has a spacey, ethereal quality that felt right for sine. From there I kept adding layers — a rhythmic layer with panning, a random crush layer that accidentally ended up sounding like percussion, and a soft chord layer underneath. The "percussion" discovery was accidental: I turned crush down to 1-2 and sine completely transformed into something grainy and rhythmic, which I liked a lot.

One thing I really enjoyed was experimenting with `vowel` — the way it filters through different vowel sounds gives the melody a more human quality. I also tried to make the sine sound like it was speaking Chinese, using `vib`, `lpq`, and different note sequences to mimic the rhythm and intonation of speech. It never quite got there, but the attempt led me to discover `attack` and `release`, which made each note feel more like a syllable — short, intentional, with a little bit of weight. That ended up shaping the melody layer a lot.

For the structure, I wanted a sense of journey — starting sparse and quiet, opening up in the middle, reaching a noisy chaotic peak with the crush layer, then collapsing back down to just the chords at the end.

Looking back, the piece ended up sounding like something I'd hear in the Japanese anime *Ikkyū-san* — which makes sense, since C:ritusen is a traditional Japanese scale. The combination of sine's pure, soft tone, the slow reverb-heavy layers, and the spacious rhythm accidentally created this very zen, temple-like atmosphere. I didn't plan for it to sound this way, but I think it's one of those happy accidents in live coding where the tools lead you somewhere unexpected and kind of wonderful.

## Technical Process

I used `stack()` to layer multiple patterns simultaneously. Key effects I used:

- `vowel` for a filter sweep that gives the melody a speaking, vocal quality
- `lpf` to control brightness
- `crush` to distort sine into something percussive
- `pan` for stereo movement
- `room` for reverb and space
- `octave` to control register
- `attack` and `release` to shape each note like a syllable
- `vib` and `lpq` for experimenting with human voice-like resonance

During performance I used `//` comments to mute and unmute layers in real time, gradually building and removing elements throughout the piece.

## Code

```javascript
stack(
  n("0 2 4 [2 3]").scale("C:ritusen").s("sine").gain(0.8).lpf(1200).vowel("<a e i o u>").lpenv(1500),
  n("0 ~ 4 ~").scale("C:ritusen").s("sine").gain(0.4).pan("<0 1>"),
  n(rand.range(0,6).segment(8)).scale("C:ritusen").s("sine").gain(0.3).crush("<20 16 14 3 2 1>"),
  
  // n("[0,2] ~ [2,4] ~").scale("C:ritusen").s("sine").gain(0.1).room(0.5).slow(2).octave(0),
  // n(rand.range(0,6).segment(8)).scale("C:ritusen").s("sine").gain(0.3).crush("<3 2 1>"),
  // n("[0,2] ~ [2,4] ~").scale("C:ritusen").s("sine").gain(0.1).room(2).slow(4).octave(0)
)
```