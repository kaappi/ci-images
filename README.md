# ci-images

Pre-built CI base images for [Kaappi Scheme](https://github.com/kaappi/kaappi).

## Images

### `ghcr.io/kaappi/builder`

Ubuntu 24.04 with Zig 0.16.0 and common build dependencies pre-installed.

**Platforms:** `linux/amd64`, `linux/arm64`

**Included:**
- Zig 0.16.0
- GCC, Make, pkg-config
- OpenSSL dev libs (for kaappi-net TLS)
- PostgreSQL client libs (for kaappi-pg)
- Redis CLI (for kaappi-redis tests)
- Git, curl

## Usage

### In CI workflows

```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    container: ghcr.io/kaappi/builder:latest
    steps:
      - uses: actions/checkout@v4
      - run: zig build && zig build test
```

### Local testing with podman

```bash
podman run --rm -v $(pwd):/src:ro ghcr.io/kaappi/builder:latest \
  bash -c 'cp -r /src /build && cd /build && zig build && zig build test'
```

### Tags

| Tag | Description |
|-----|-------------|
| `latest` | Latest stable build |
| `zig-0.16.0` | Pinned to Zig 0.16.0 |
