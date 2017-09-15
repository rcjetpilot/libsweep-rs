# libsweep-rs

[![Version](https://img.shields.io/crates/v/libsweep.svg)](https://crates.io/crates/libsweep)
[![Docs](https://docs.rs/libsweep/badge.svg)](https://docs.rs/libsweep)

This is a Rust wrapper for the Sweep SDK for interacting with the Scanse Sweep LIDAR unit.

```rust
let port = String::from("/dev/tty.usbserial-DM00KC6Z");
let sweep = Sweep::new(port).unwrap();
sweep.start_scanning().unwrap();
let points = sweep.scan().unwrap();
for point in &points {
    println!("Angle {}, Distance {}, Signal Strength: {}",
        point.angle, point.distance, point.signal_strength);
}
sweep.stop_scanning().unwrap();
```

# Instructions

- Clone the repo at https://github.com/scanse/sweep-sdk and follow build instructions
- Build this crate with `cargo build`
- For now, modify the source code with the correct path to the lidar unit ... test is hardcoded to /dev/ttyUSB0
- Connect the Sweep unit and run `cargo test --nocapture` to see measurements

You should see output like:

```
sweep_is_abi_compatible returned true
sweep_get_version returned 65538
constructing device
Motor speed: 5
Sample rate: 500
start scanning
Angle 202062, Distance 23, Signal Strength: 199
Angle 204625, Distance 24, Signal Strength: 191
Angle 208125, Distance 22, Signal Strength: 175
Angle 220375, Distance 650, Signal Strength: 167
Angle 222937, Distance 380, Signal Strength: 191
Angle 225125, Distance 373, Signal Strength: 199
stop scanning
test tests::ffi_calls_work ... ok
```



