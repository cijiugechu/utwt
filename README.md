# `utwt`

[![Crates.io](https://img.shields.io/crates/v/utwt.svg)](https://crates.io/crates/utwt)
[![Docs](https://docs.rs/utwt/badge.svg)](https://docs.rs/utwt)

<!-- cargo-sync-readme start -->

A Rust crate for parsing `utmp` files like `/var/run/utmp` and `/var/log/wtmp`.

> Note: This project has been forked from [utmp-rs](https://github.com/upsuper/utmp-rs) since September of 2023, but a lot has changed.

## Usage

Simplest way is to use `parse_from_*` functions,
which returns a `Vec<UtmpEntry>` on success:
```rust
let entries = utwt::parse_utmp()?;
// or specify a path explicitly
let entries = utwt::parse_from_path("/var/run/utmp")?;
//
```

If you don't need to collect them all,
`UtmpParser` can be used as an iterator:
```rust
use utwt::UtmpParser;
for entry in UtmpParser::from_path("/var/run/utmp")? {
    let entry = entry?;
    // ...
}
```

All the `parse_from_*` functions as well as `UtmpParser` parse `utmp` file
based on the native format for the target platform.
If cross-platform parsing is needed,
`Utmp32Parser` or `Utmp64Parser` can be used instead of `UtmpParser`.

<!-- cargo-sync-readme end -->
