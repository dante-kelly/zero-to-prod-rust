# zero-to-prod-rust

In the world of programming, you either die on the JavaScript hill or you live long enough to become a Rustacean

## What is this?

This is a development project on progress from the book Zero to Production in Rust. I will most likely add additional
abstract test code to supplement learning in this book.

## How to run

1. Install rust through https://rustup.rs/.
2. `cd` into the desired project folder.
3. Run `cargo run` to run the project.

## How to watch changes

1. Run cargo watch, and optionally link, with `cargo watch -x check -t test -x run`.

## How to add crates

- Add the crate to the `Cargo.toml` file.
- OR run `cargo add <crate_name>` to add the crate to the `Cargo.toml` file.

## How to inspect code

- Run 'cargo expand' to expand macros.
- For Tests: Run `cargo expand --test rust_file`.