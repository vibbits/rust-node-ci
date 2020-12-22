##
## This is the base Rust/Node image for CI.
## Other images in this repository are built on
## top of this image.
##

FROM node:15.4.0-buster

# make Apt non-interactive
RUN echo 'APT::Get::Assume-Yes "true";' > /etc/apt/apt.conf.d/90vibbioinfocore \
  && echo 'DPkg::Options "--force-confnew";' >> /etc/apt/apt.conf.d/90vibbioinfocore

ENV DEBIAN_FRONTEND=noninteractive
MAINTAINER VIB Bioinformatics Core Facility

# man directory is missing in some base images
# https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=863199
RUN apt-get update \
  && mkdir -p /usr/share/man/man1 \
  && apt-get install -y \
    git mercurial xvfb apt \
    locales sudo openssh-client ca-certificates tar gzip parallel \
    net-tools netcat unzip zip bzip2 gnupg curl wget make


# Set timezone to UTC by default
RUN ln -sf /usr/share/zoneinfo/Etc/UTC /etc/localtime

# Use unicode
RUN locale-gen C.UTF-8 || true
ENV LANG=C.UTF-8

# Install rust
# https://github.com/rust-lang/rustup/issues/1085
ENV RUSTUP_HOME=/opt/rust \
    CARGO_HOME=/opt/rust
RUN RUSTUP_URL="https://sh.rustup.rs" \
  && curl --silent --show-error --location --fail --retry 3 --proto '=https' --tlsv1.2 --output /tmp/rustup-linux-install.sh $RUSTUP_URL \
  && bash /tmp/rustup-linux-install.sh -y --no-modify-path

RUN groupadd --gid 3434 vibbioinfocore \
  && useradd --uid 3434 --gid vibbioinfocore --shell /bin/bash --create-home vibbioinfocore \
  && echo 'vibbioinfocore ALL=NOPASSWD: ALL' >> /etc/sudoers.d/50-vibbioinfocore \
  && echo 'Defaults    env_keep += "DEBIAN_FRONTEND"' >> /etc/sudoers.d/env_keep


# IMAGE CUSTOMISATIONS

RUN /opt/rust/bin/rustup target add x86_64-pc-windows-msvc

USER vibbioinfocore
ENV PATH /opt/rust/bin:${PATH}

CMD ["/bin/sh"]