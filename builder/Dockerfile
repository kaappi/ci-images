FROM ubuntu:24.04

ARG ZIG_VERSION=0.16.0
ARG TARGETARCH

RUN apt-get update -qq && \
    apt-get install -y -qq --no-install-recommends \
      curl xz-utils ca-certificates git make gcc libc6-dev pkg-config \
      libssl-dev libpq-dev redis-tools postgresql-client && \
    rm -rf /var/lib/apt/lists/*

RUN case "${TARGETARCH}" in \
      amd64) ZIG_ARCH=x86_64 ;; \
      arm64) ZIG_ARCH=aarch64 ;; \
      riscv64) ZIG_ARCH=riscv64 ;; \
      *) echo "Unsupported arch: ${TARGETARCH}" && exit 1 ;; \
    esac && \
    curl -sL "https://ziglang.org/download/${ZIG_VERSION}/zig-${ZIG_ARCH}-linux-${ZIG_VERSION}.tar.xz" \
      | tar xJ -C /opt && \
    ln -s /opt/zig-*-linux-*/zig /usr/local/bin/zig

RUN zig version

WORKDIR /build
