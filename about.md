# About Wickra Pico

Wickra Pico runs Wickra's O(1) indicator core bare-metal on a $5 Raspberry Pi
Pico. An embedded replay feed streams tick-by-tick through the `no_std` Wickra
signal kernel — an EMA(9)/EMA(21) cross — and on a signal, a GPIO LED toggles. It
is a **hardware showcase, not a library**: there is nothing to install from a
package registry.

## What makes it different

- **No OS, no allocator, no heap.** No other technical-analysis stack runs without
  an operating system. Wickra Pico runs the indicator math `no_std` on an RP2040 —
  `forbid(unsafe_code)`, allocation-free.
- **The LED blinks on the cross.** The whole demo: an embedded replay feed drives
  the `no_std` kernel, and a GPIO LED toggles on the EMA cross.
- **Byte-identical to the host.** The on-device signal sequence is verified
  byte-identical to a `std` host reference — cross-target determinism, the same
  guarantee the rest of the ecosystem makes across languages.
- **The wickra-embed kernel.** The `no_std` indicator kernel comes from
  [`wickra-embed`](https://github.com/wickra-lib/wickra-embed) (allocation-free,
  `#![no_std]`, `forbid(unsafe_code)`), consumed as a git dependency.

## Why it exists

It is a proof: the exact same indicator math that powers backtests, feature builds and
live charts across ten languages also runs on a microcontroller with a few KB of
RAM — no operating system, no reimplementation, no drift. The blinking LED is the
visible end of a determinism contract that runs all the way down to bare metal.

## Open source

Released under the **MIT OR Apache-2.0** license — permissive, OSI-approved, free
for any use including commercial. Source, firmware releases and the demo on
[GitHub](https://github.com/wickra-lib/wickra-pico).

## Disclaimer

Wickra Pico is a hardware demo, **not** a trading system, and is provided **as-is
with no warranty**. It blinks an LED on a synthetic replay feed; it does not give
financial advice. Use it at your own risk.
