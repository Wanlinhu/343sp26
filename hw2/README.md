# MiniTidal Percussion Patch

**Name:** Wanlin Huang  
**Environment:** Estuary (MiniTidal)  
**Samples used:** bd sd hh lt cp  
**Tempo:** 120 BPM (set in Estuary terminal)

---

## Percussion Patch

```haskell
stack [
  s "bd bd ~ bd bd [bd ~] bd ~ ~ sd ~ sd ~ sd ~ sd"
    # gain 1,
  s "hh ~ hh hh hh ~ hh hh"
    # gain 0.7,
  s "~ cp ~ cp ~ cp cp ~"
    # gain 0.8,
  s "~ ~ lt ~ ~ ~ [lt ~] ~"
    # gain 0.75
]
```

---

## What I Made

I made a layered percussion patch using only the five starter drum samples: bd, sd, hh, lt, and cp. I wanted it to feel groovy and stable — something I'd actually enjoy listening to on loop, not just something that shows off a bunch of syntax.

## How I Approached It

I started with kick and snare because they set the groove. Once that felt good, I layered in hi-hats for motion, claps for accents, and low toms as subtle fills. At each step I just listened and asked myself: does this still feel good, or am I adding things just because I can? If it started feeling cluttered, I took stuff out.

## Creative Process

Honestly, I tried a lot of the things from the class notes at first — different operators, `every`, `fast`, `speed`, all of that. A lot of it threw syntax errors or just didn't behave the way I expected in Estuary. After a while I stopped fighting it and just leaned into simplicity. I think a pattern that actually feels good is more interesting than a complicated one that feels like a mess. Once I found something that sounded solid, I stopped adding more — because every time I added another layer it actually got worse, not better.

## Technical Process

I used `stack` to combine all four rhythmic layers into one pattern. Each layer is just `s "..."` with `~` for silence and bracket groups like `[bd ~]` and `[lt ~]` to squeeze multiple hits into one pulse. I set the tempo to 120 BPM in the Estuary terminal with `!setbpm 120`, and balanced the mix with `# gain` — kick and snare at full, hi-hats a bit quieter in the background, clap slightly louder for accent, and low tom kept subtle so it doesn't take over.

## Reflection

This assignment made me realize that musical clarity matters more than using advanced syntax. Even with just five drum sounds I was able to make something that feels alive and usable. It also made me see that debugging and simplifying are part of the creative process — not a sign that something went wrong.
