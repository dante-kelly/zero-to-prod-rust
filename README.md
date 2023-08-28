# Zero to Production in Rust

![Rust](https://img.shields.io/badge/Rust-1.72-brightgreen.svg)
![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)
![Build Status](https://github.com/dante-kelly/zero-to-prod-rust/actions/workflows/general.yml/badge.svg)
![Last Commit](https://img.shields.io/github/last-commit/dante-kelly/zero-to-prod-rust)
![Code Size](https://img.shields.io/github/languages/code-size/dante-kelly/zero-to-prod-rust)


> "In the world of programming, you either die on the JavaScript hill or you live long enough to become a Rustacean."

## 📌 Table of Contents

- [About](#about)
- [Technology Stack](#technology-stack)
- [Security](#security)
- [Getting Started](#getting-started)
    - [Prerequisites](#prerequisites)
    - [Installation](#installation)
- [Usage](#usage)
    - [Running the Project](#running-the-project)
    - [Watching Changes](#watching-changes)
    - [Adding Crates](#adding-crates)
    - [Code Inspection](#code-inspection)
- [Database](#database)
    - [Using Docker for Postgres](#using-docker-for-postgres)
    - [Interacting with the Database](#interacting-with-the-database)
- [Deployment](#deployment)
    - [Building for Production](#building-for-production)
    - [Setting up Kubernetes Locally](#setting-up-kubernetes-locally)
- [TODO](#todo)
- [Contributing](#contributing)
- [License](#license)

## 📜 About

This project is based on the book "Zero to Production in Rust". It aims to build a stable, secure, and production-ready
Kubernetes microservices cluster using the latest stable Rust and its dependencies.

## 🛠 Technology Stack

This project is built with some of the latest technologies and services to provide a robust, scalable, and efficient
application. Below are the core technologies used:

### 🦀 Rust

- The project is primarily written in Rust, offering memory safety and performance.

### 🐳 Kubernetes

- Kubernetes is used for automating deployment, scaling, and management of containerized applications.

### 🐘 PostgreSQL

- PostgreSQL is used as the primary database, known for its reliability and robustness.

## 🔒 Security

Security is a top priority in this project. With the increasing number of vulnerabilities found in various Docker
images, it's crucial to limit potential attack vectors. Many Docker images come with unnecessary software and libraries
that not only increase the image size but also introduce potential vulnerabilities. Keep in mind, this is a project
meant to have fun in and try new things, so errors will be made, especially during the early stages. One example being
the passes being stores in plain text and data remaining unencrypted. This will ideally be fixed in the future.

### Hardened Docker Images by RapidFort

To mitigate these risks, wherever possible, we use hardened Docker images provided by RapidFort. These images are
stripped down to contain only the essential software and libraries, reducing the attack surface while also being
optimized for performance.

By taking these precautions, we aim to make the application not only robust but also secure against various types of
vulnerabilities.

## 🚀 Getting Started

### Prerequisites

- Install Rust through [rustup](https://rustup.rs/).

### Installation

1. Clone the repository.
2. `cd` into the project folder.
3. Run `cargo run` to start the project.

## 🛠 Usage

### Running the Project

```bash
cargo run
```

For better logging:

```bash
TEST_LOG=true cargo run | bunyan
```

### Watching Changes

Run the following command to watch for changes:

```bash
cargo watch -x check -x test -x run
```

### Adding Crates

- Add the crate to the `Cargo.toml` file.
- OR run `cargo add <crate_name>` to add the crate automatically.

### Code Inspection

- Expand macros: `cargo expand --bin {rust_target}`
- For tests: `cargo expand --test {rust_file}`

## 🗄 Database

### Using Docker for Postgres

1. `cd` into the 'scripts' folder.
2. Launch Postgres with `./scripts/init_db.sh`.
3. To stop the containers, run `docker-compose down`.

### Interacting with the Database

- Use PgAdmin through Docker after manual setup.
- Use CLI: `psql -h localhost -p 5432 -U postgres -d zero2prod`
- Use sqlx-cli: `cargo sqlx {cool_commands}`

## 🚢 Deployment

### Building for Production

```bash
docker build --tag zero2prod --file Dockerfile .
docker run -p 8000:8000 zero2prod
```

### Setting up Kubernetes Locally

1. Install [minikube](https://minikube.sigs.k8s.io/docs/start/).
2. Start minikube: `minikube start`.
3. Create namespaces:
   ```bash
   kubectl create namespace rust-api-gateway
   kubectl create namespace postgres-database
   ```
4. Add docker environment to minikube: `eval $(minikube docker-env)`
5. `cd` into the 'k8s-manifests' folder.
6. Apply manifests: `kubectl apply -f . -n rust-api-gateway`

## 📝 TODO

- [ ] Add proper Kubernetes local development environment.
- [ ] Add easier scripts for Kubernetes setup.
- [ ] Implement Kubernetes service communication.
- [ ] Integrate third-party Kubernetes secrets manager.
- [ ] Deploy to a third-party Kubernetes cluster.
- [ ] Implement CI/CD for Kubernetes.
- [ ] Integrate monitoring, logging, and performance tools.
- [ ] Improve documentation.
- [ ] Add documentation graphics.
- [ ] Implement auto-generated documentation.
- [ ] Consider alternatives to minikube.

## 🤝 Contributing

Contributions are welcome! See [CONTRIBUTING.md](CONTRIBUTING.md) for more details.
