# Hydra Patch — Ink Wash

## What I did

Webcam input processed to look like water ink painting.

## Creative process

First attempts were too colorful and busy — the default Hydra rainbow aesthetic. I wanted something calmer that could sit behind a musician without competing for attention.

Water ink painting came to mind. Growing up around 水墨, there's something immediately familiar about that aesthetic — the way ink bleeds into wet paper, how a single brushstroke can feel both controlled and accidental at the same time. What I didn't expect was how naturally Hydra could recreate that feeling. `modulateScale` with slow noise actually behaves like ink diffusing in water — it's not simulating it, it just ends up looking that way. That surprise was the most fun part. It felt less like programming and more like playing with a new material, nudging parameters and watching something unexpected bleed through.

## Technical process

```javascript
s0.initCam()

src(s0)
  .saturate(0.15)                      // crush color to near-greyscale
  .brightness(0.05)
  .modulateScale(noise(8, 0.1), 0.3)   // slow fluid distortion
  .thresh(0.5, 0.04)                   // hard edges like ink
  .add(
    osc(18, 0.03).saturate(0.15).mult(noise(8)),
    0.15                               // faint texture layer
  )
  .out(o0)
```

`saturate(0.15)` does most of the aesthetic work. `modulateScale` with slow noise creates the fluid feeling. `thresh` is what makes it look like ink rather than just a filtered webcam.

## What I'd try next

- Routing audio (`a.fft`) into the `thresh` tolerance so edges harden with the music
- `initScreen` instead of cam — ink wash on a score could be interesting