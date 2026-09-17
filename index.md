---
layout: home
title: Wickra Pico — the indicator core, bare-metal on a $5 chip
titleTemplate: false

hero:
  name: "Wickra Pico"
  text: "The LED blinks on the EMA cross."
  tagline: "Wickra's O(1) indicator core running bare-metal on a $5 Raspberry Pi Pico — an embedded replay feed streams tick-by-tick through the no_std kernel, and on a signal a GPIO LED toggles. A hardware showcase, not a library."
  image:
    src: /wickra-mark.svg
    alt: Wickra Pico
  actions:
    - theme: brand
      text: View on GitHub
      link: https://github.com/wickra-lib/wickra-pico
    - theme: alt
      text: Flash the firmware
      link: https://github.com/wickra-lib/wickra-pico/releases
    - theme: alt
      text: Live demo
      link: /demo

features:
  - icon: 💡
    title: The LED blinks on the cross
    details: An embedded replay feed streams tick-by-tick through the no_std Wickra signal kernel — an EMA(9)/EMA(21) cross. On a signal, a GPIO LED toggles. That is the whole demo, and it needs no operating system.
  - icon: 🔩
    title: No OS, no allocator, no heap
    details: "No other technical-analysis stack runs without an operating system. Wickra Pico runs the indicator math no_std on a $5 RP2040 — no OS, no allocator, no heap, forbid(unsafe_code)."
  - icon: 🎯
    title: Byte-identical to the host
    details: "The on-device signal sequence is verified byte-identical to a std host reference — cross-target determinism, the same guarantee the rest of the ecosystem makes across ten languages."
  - icon: 🧩
    title: The wickra-embed kernel
    details: "The no_std indicator kernel comes from wickra-embed's 5 indicators (allocation-free), consumed as a git dependency — the same math that powers the full std Wickra library, distilled to bare metal."
  - icon: 💾
    title: Flash it in seconds
    details: "A release builds a flashable RP2040 firmware image (.uf2). Hold BOOTSEL, drag the file onto the drive that appears, and the Pico starts replaying — no toolchain required to run it."
  - icon: 🧪
    title: Deterministic, proven
    details: The firmware's signal sequence is pinned against a std host reference in CI, so the bare-metal path and the cloud path never disagree — the same determinism contract, on silicon.
---

## The whole thing, in one loop

Wickra Pico is a **hardware showcase, not a library**. There is nothing to install
from a package registry — it is firmware. An embedded replay feed streams
tick-by-tick through the `no_std` Wickra signal kernel (an EMA(9)/EMA(21) cross);
on a signal, a **GPIO LED toggles**.

```rust
#![no_std]
#![no_main]

// Pseudocode of the firmware hot loop.
let mut cross = EmaCross::new(9, 21);

loop {
    let tick = feed.next();          // embedded replay feed
    if let Some(signal) = cross.update(tick) {
        led.toggle();                // the whole demo: an LED on the cross
    }
}
```

The kernel is `no_std`, allocation-free and `forbid(unsafe_code)` — the same
indicator math the full Wickra library runs, distilled down to what fits on a
microcontroller.

## Flash it

A GitHub release builds a flashable **RP2040 firmware image** (`.uf2`):

1. Download the latest `.uf2` from
   [releases](https://github.com/wickra-lib/wickra-pico/releases).
2. Hold **BOOTSEL** on the Pico and plug it in — it mounts as a USB drive.
3. Drag the `.uf2` onto the drive. The Pico reboots and starts replaying.

No Rust toolchain is needed to run it; the firmware is built for you in CI.

## Built on the Wickra core

Wickra Pico's kernel comes from
[`wickra-embed`](https://github.com/wickra-lib/wickra-embed) — the allocation-free,
`no_std` distillation of [`wickra-core`](https://github.com/wickra-lib/wickra). The
indicator values on the chip are byte-identical to the ones a server or a live
chart would compute.

> Wickra Pico is a hardware demo, not a trading system, and comes with no warranty —
> use at your own risk.
