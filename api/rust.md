# Rust

The native crate — the same engine every other binding of Wickra Pico wraps.

```bash
cargo add None
```

```rust
let mut engine = SignalEngine::new();
for &price in embedded_data::FEED.iter() {
    match engine.on_tick(f64::from(price)) {
        Some(Signal::GoldenCross) => led.set_high().unwrap(),
        Some(Signal::DeathCross)  => led.set_low().unwrap(),
        None => {}
    }
    delay.delay_ms(60);
}
```

## More

- [crates.io/crates/None](https://crates.io/crates/None)
- [docs.rs](https://docs.rs/None)
- [Source & examples](https://github.com/wickra-lib/wickra-pico/tree/main/examples)
