# kubeless-rs #
[![Crates.io](https://img.shields.io/crates/v/kubeless.svg)](https://crates.io/crates/kubeless)
[![Crates.io](https://docs.rs/kubeless/badge.svg)](https://docs.rs/kubeless)

A Rust library for writing [Kubeless](https://kubeless.io) functions.

## Example ##
```rust
#[macro_use]
extern crate kubeless;

fn say_hello(event: kubeless::Event, ctx: kubeless::Context) -> String {
    match event.data {
        Some(name) => format!("Hello, {}", String::from_utf8_lossy(&name)),
        None => String::from("Hello"),
    }
}

fn say_goodbye(event: kubeless::Event, ctx: kubeless::Context) -> String {
    match event.data {
        Some(name) => format!("Goodbye, {}", String::from_utf8_lossy(&name)),
        None => String::from("Goodbye"),
    }
}

fn main() {
    kubeless::start(select_function!(say_hello, say_goodbye));
}
```