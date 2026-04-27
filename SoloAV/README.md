# Live Coding Session

## Code Documentation

### Hydra — Visual

```js
osc(0, 10, 1.7)
// oscillator: freq=0, speed=10, color offset=1.7 → colored static base texture

.diff(osc(0, 0.03, 1.7).rotate(1.57))
// subtract a slow-moving osc rotated 90° → creates grid interference pattern

.mult(osc(0, 0.001, 0).rotate(2))
// multiply by a nearly frozen black/white osc rotated ~115° → adds depth layering

.blend(o0, 0.94)
// mix with previous frame at 94% → long trail / feedback loop

.modulateScale(osc(0, 0.01), -0.01)
// micro-distortion using slow osc → subtle surface trembling

.scale(0.8, () => (1.05 + 0.1 * Math.abs(Math.sin(4 * time))))
// x compressed to 80%, y breathes slowly with sin wave

.out(o0)
// output → feeds back into blend above, closing the loop
```

---

### Strudel — Audio

```js
setcps(66/120)  // tempo: 66 BPM (expressed as ratio to 120 BPM grid)

// — CHORD PAD (commented out) —
// $: note("<[e3,b3,d4] [b2,f#3,a3] [c3,g3,b3] [g2,b2,d3,g3]>")
// cycling 4-chord progression: Em → Bm → Cmaj → Gmaj voicings
//    .s("<triangle sine>")   // alternates between two soft timbres
//    .slow(4)                // each chord lasts 4 cycles
//    .sustain(4).attack(1.5).gain(2).room(1)  // slow swell, spacious reverb

// — MELODY (commented out) —
// $: note("e4 ~ ~ g4 ~ a4 ~ ~ ~ b4 ~ a4")
// sparse melodic line with rests (~), floating on top
//    .s("triangle")
//    .vowel("<a o u e>")     // vowel filter cycles → talking/formant quality
//    .slow(2)
//    .delay(0.3).delaytime(0.375).delayfeedback(0.25)  // rhythmic echo
//    .room(0.92)             // near-wet reverb

// — BASS (partially active) —
// $: note("<e2 b1 c2 g1>")  // root notes matching chord progression
//    .s("sine")              // pure sine = sub bass feel
//    .slow(4)
//    .lpf(perlin.slow(8).range(200, 500))  // filter breathes with Perlin noise
//    .gain(0.35)
   .room(2)                  // ← only this line is active (very wet reverb tail)

// — KICK (commented out) —
// $: s("bd ~ ~ ~ ~ ~ ~ bd ~ ~ ~ ~ ~ ~ ~")  // sparse kick, every 8 steps
//    .gain(0.4)
```

---

## Reflection

I found it quite challenging to edit visuals and audio simultaneously while performing live. Working on both at the same time means they are constantly taking turns — when one gets your attention, the other quietly waits. The Hydra kept running. Most of the Strudel patterns stayed commented out.

Before this class I didn't know music could be made this way — writing code that plays, watching patterns shift in real time, nothing fixed. If I'd known earlier that coding could get me here, I probably would have started sooner.
