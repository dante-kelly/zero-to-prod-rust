# Using a branch I've seen the vulnerabilities of, to prevent unknown vulnerabilities in latest.
# This requires more diligency and CI/CD to ensure we're not using a vulnerable version of Rust.
FROM lukemathwalker/cargo-chef:latest-rust-1.72 AS chef
WORKDIR /app
RUN apt update && apt install lld clang -y

FROM chef AS planner
COPY . .
# Compute a lock-like file for our project dependencies
RUN cargo chef prepare --recipe-path recipe.json

FROM chef AS builder
COPY --from=planner /app/recipe.json recipe.json
# Build ONLY our project dependencies
RUN cargo chef cook --release --recipe-path recipe.json
COPY . .
ENV SQLX_OFFLINE true
# Start building our project, using the pre-built deps
RUN cargo build --release

# Using a newer version of Debian to limit vulnerabilities. Testing is necessary.
# Appropriate fallback is debian:bullseye-slim
FROM debian:bookworm-slim AS runtime
WORKDIR /app
RUN apt-get update -y \
    && apt-get install -y --no-install-recommends openssl ca-certificates \
    # Clean up
    && apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*
COPY --from=builder /app/target/release/zero2prod zero2prod
COPY configuration configuration
ENV APP_ENVIRONMENT production
ENTRYPOINT ["./zero2prod"]