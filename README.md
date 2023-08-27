# Zero to Production in Rust

In the world of programming, you either die on the JavaScript hill or you live long enough to become a Rustacean

## What is this?

This is a development project based on the book Zero to Production in Rust, using latest stable Rust and
dependencies. The goal is to eventually build a very stable and secure, production ready Kubernetes microservices
cluster within Rust.

## How to run

1. Install rust through https://rustup.rs/.
2. `cd` into the desired project folder.
3. Run `cargo run` to run the project.
4. For better logging use `TEST_LOG=true cargo run | bunyan`.

## How to watch changes

1. Run cargo watch, and optionally link, with `cargo watch -x check -x test -x run`.

## How to add crates

- Add the crate to the `Cargo.toml` file.
- OR run `cargo add <crate_name>` to add the crate to the `Cargo.toml` file.

## How to inspect code

- Run `cargo expand --bin {rust_target}` to expand macros.
- For Tests: Run `cargo expand --test {rust_file}`.

## How to use Docker to run Postgres

- cd into the 'scripts' folder
- Launch Postgres with `./scripts/init_db.sh`
- Run `docker-compose down` to stop the containers

## How to build for production

1. Run `docker build --tag zero2prod --file Dockerfile .`
2. Run `docker run -p 8000:8000 zero2prod`

## How to interact with the Database

- The Database can be touched from PgAdmin through Docker after manually setting up PgAdmin.
- OR you can use the CLI with `psql -h localhost -p 5432 -U postgres -d zero2prod`
- OR you can use sqlx-cli with `cargo sqlx {cool_commands}` after exporting the DATABASE_URL environment variable.
  with `export DATABASE_URL=postgres://root:toor@127.0.0.1:5432/newsletter`

## TODO

1. Add Kubernetes.
2. Add better local logging with bunyan.
3. Deploy a logging, performance, and error monitoring system.