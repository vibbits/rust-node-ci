# Rust/node docker images for Continuous Integration
Docker images optimized for building Rust and Node projects in CI.

* rust-node: The base image.
* rust-elm: An image for building Rust and Elm projects.

## Releasing

Docker Hub has put automatic releases behind a paywall so here are the release instructions:

1. Update the dockerfiles as necessary
1. Ensure you're logged in as the vibbioinfocore user
1. in `rust-node/` run: `docker build -t vibbioinfocore/rust-node-ci:latest .`
1. Ensure versions are correct with: `docker run vibbioinfocore/rust-node-ci:latest .`
1. Push with: `docker push vibbioinfocore/rust-node-ci:latest`
1. Switch to `rust-elm/`
1. Build with: `docker build -t vibbioinfocore/rust-node-ci:elm .`
1. Ensure versions are correct with: `docker run vibbioinfocore/rust-node-ci:elm .`
1. Push with: `docker push vibbioinfocore/rust-node-ci:latest`
1. Check docker Hub: `https://hub.docker.com/r/vibbioinfocore/rust-node-ci`
1. Update the DockerHub README with the new versions
