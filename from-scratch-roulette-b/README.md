# From Scratch Roulette B — Reflection
**Due: Mon Apr 13, 2026**

## Reflection

Today's From Scratch Roulette B was one of my favorite experiences so far. I collaborated with Neil — he handled the audio while I worked on the visuals using Hydra, and it was my first time doing live coding with Hydra in a real performance context.

Coming into this after Roulette A, I already had a sense of how flexible Hydra could be, but working live pushed that understanding further. I was surprised by how much you can do in real time — layering, muting, shifting colors and speeds on the fly — and how the structure of Hydra code feels surprisingly similar to how audio is built up in layers. Adding a source, muting a layer, chaining effects — it maps almost directly onto how Neil was building his stack in Strudel.

One thing I discovered was using Hydra's `speed` variable to match the energy of Neil's audio in the moment. When he pushed the rhythm forward I could change one number and the whole visual would follow — that kind of instant synchronization felt really powerful.

Being live also meant dealing with small errors in the moment — variables not found, chains breaking because of a missing dot. But I actually think that's part of what makes live coding interesting as a performance. The mistakes are visible, and fixing them in real time is its own kind of improvisation.

What struck me most was how naturally the collaboration flowed. When I heard Neil's audio, images and textures would come to mind almost immediately, and I found myself translating that into visual decisions in the moment. That kind of instant response felt really exciting.

This session also made me realize that I'm genuinely more drawn to the visual side of live coding than I expected. And honestly, it's what made me want to sign up for the Saturday performance.

---

## Code Documentation

### Neil's Strudel (Audio)

```javascript
setcps(80 / 60 / 4); // 80 BPM

// 1. Drum groove
const drums = stack(
  s("[bd]*8 [~ ~ ~ bd] [bd ~ ~ ~] [~ ~ bd ~]"),
  s("[~] [~ sd ~ ~] [sd] [~ ~ sd sd]")
).bank("jd990");

// 2. Keyboard progression (8-chord cycle, finishes in 4 bars)
let myProgression = "<[0, 7, 11, 16] [-1, 7, 14, 19] [-3, 7, 12] [-3, 7, 13] [2, 9, 12, 17] [-5, 5, 9, 12, 16] [0, 7, 11, 16] [0, 7, 11, 16]> * 2";
const keys = note(myProgression)
  .s("gm_epiano2")
  .transpose(60);

let root = "<[0] [-1] [-3] [-3] [2] [-5] [0] [0]> * 2";
const bass = note(root)
  .s("gm_fretless_bass")
  .transpose(48);

const melody = note(scale("C:major:pentatonic", irand(10)))
  .struct("x(4,8) [- x ~ x] x*2 ~")
  .s("gm_marimba")
  .transpose(12)
  .decay(0.15).sustain(0)
  .gain(0.7);

const melody2 = note(scale("G:major:pentatonic", irand(10)))
  .struct("x(2,4) [x x x]*4 x*8 ~")
  .s("gm_pad_warm")
  .transpose(12)
  .decay(0.15).sustain(0)
  .gain(0.7);

const melody3 = note(scale("C:major:pentatonic", irand(10)))
  .struct("x(4,8) [- x ~ x] x*2 ~")
  .s("gm_pad_choir")
  .transpose(24)
  .decay(0.15).sustain(0)
  .gain(1);

stack(drums, keys, bass, melody, melody2, melody3)
```

---

### My Hydra (Visual)

```javascript
speed = 0.1; // global speed — change this to match Neil's energy

osc(20, 0.1, 0).color(0, 1, 2).rotate(1/2).out(o1);

// random shapes layer
shape([5,4,5,6].fast(1).smooth(1), 0.5, 0.01)
  .color(() => Math.random(), () => Math.random(), () => Math.random())
  .repeat(1, 3)
  .out(o2);

// main chain
osc(4, 0.1, 1)
  .color(5, 0.7, 1)
  .modulate(o1, 0)
  .add(o1, 1)
  .modulatePixelate(o1, , 1)
  .add(
    voronoi(1, 2, 10)
    .color(0.2, 0.6, 0.5)
    .scrollX(() => Math.sin(time * 0.155))
    .scrollY(() => Math.cos(time * 0.23))
    , 0.3)
  .add(
    noise(100000, 4)
    .thresh(0.85, 0.01)
    .color(1.8, 1.5, 2)
    .scrollX(() => Math.sin(time * 0.4))
    , 100)
  .add(src(o2), 0)  // random shapes — change 0 to add
  .add(
    src(o0)
    .scale(0.98)
    .rotate(0.001)
    , 0.01)
  .out(o0)
```

### Live coding strategy

| Layer | How to mute | Effect |
|---|---|---|
| `voronoi` | `.add(voronoi(...), 0)` | organic texture disappears |
| `noise` | `.add(noise(...), 0)` | sparkle points disappear |
| random shapes | `.add(src(o2), 0)` | colour flashes disappear |
| feedback | `.add(src(o0)..., 0)` | trail effect disappears |
| global speed | `speed = 2` | everything speeds up |
| osc lines | `rotate(0)` / `rotate(1.57)` | vertical / horizontal lines |