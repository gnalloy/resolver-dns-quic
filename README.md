# resolver-dns-quic

[简体中文](README.zh-CN.md) | [Documentation](docs/README.md)

DNS-over-QUIC exchanger for Gnalloy resolver using RFC 9250 ALPN doq over QUIC streams.

This module provides name-resolution building blocks for higher-level transports and clients. It keeps DNS message parsing, exchange policy, timeout, and cache concerns explicit.

## Status

- Import path: `gnalloy.org/resolver-dns-quic`
- Repository: `github.com/gnalloy/resolver-dns-quic`
- Default branch: `dev`
- Preview install: `go get gnalloy.org/resolver-dns-quic@dev`
- License: Apache-2.0

## Install
```bash
go get gnalloy.org/resolver-dns-quic@dev
go doc gnalloy.org/resolver-dns-quic
GOWORK=off GOTOOLCHAIN=local go test ./... -count=1
```

## Documentation
- [Overview](docs/overview.md) ([中文](docs/overview.zh-CN.md))
- [Usage](docs/usage.md) ([中文](docs/usage.zh-CN.md))
- [Examples](docs/examples.md) ([中文](docs/examples.zh-CN.md))
- [Configuration](docs/configuration.md) ([中文](docs/configuration.zh-CN.md))
- [Testing and Performance](docs/testing.md) ([中文](docs/testing.zh-CN.md))
- [API Reference](docs/api.md) ([中文](docs/api.zh-CN.md))
- [Notes and Caveats](docs/notes.md) ([中文](docs/notes.zh-CN.md))
- [ADR-001 Module Boundary](docs/decisions/0001-module-boundary.md) ([中文](docs/decisions/0001-module-boundary.zh-CN.md))

## Module Boundary

This repository owns: DNS-over-QUIC exchanger for Gnalloy resolver using RFC 9250 ALPN doq over QUIC streams.

It does not absorb neighboring module responsibilities. Core primitives stay in `gnalloy.org/gnalloy`; protocol codecs, transports, handlers, resolvers, examples, and benchmarks stay in their own repositories.

## Packages
- `gnalloy.org/resolver-dns-quic` (`quic`)

## Gnalloy Dependencies
- `gnalloy.org/codec-dns`
- `gnalloy.org/resolver-dns`
- `gnalloy.org/transport-quic`

## Common Integration Pattern
- Configure upstream name servers, exchange timeout, cache policy, search domains, and hosts overrides according to the caller environment.
- Network transport for DNS is explicit: UDP, TCP fallback, or QUIC depending on the resolver module in use.
- QUIC and HTTP/3 paths require TLS 1.3 and a valid ALPN such as `h3`, `doq`, or the WebTransport profile in use.

## Current Public Entry Points

The generated API reference lists the full public surface. Common constructors or option types currently include:
- `const DefaultALPN = "doq" ...`

## Verification

```bash
GOWORK=off GOTOOLCHAIN=local go test ./... -count=1
GOWORK=off GOTOOLCHAIN=local go vet ./...
GOWORK=off GOTOOLCHAIN=local go test ./... -run '^$' -bench . -benchmem -count=1
```

For pressure tests, assemble this module with the relevant transport, codec, and handler stack and run the scenario from `gnalloy.org/benchmarks` or `gnalloy.org/examples`. Keep host, operating system, payload, concurrency, warmup, and repetitions in the report.

## Caveats
- This repository is intentionally narrow. Cross-module behavior should be assembled in applications, recipes, examples, or benchmark harnesses.
- Public APIs should remain Go-native and explicit; avoid runtime scanning, hidden global registries, and reflection-heavy behavior in hot paths.
- Treat network input as untrusted. Configure parser limits and return typed errors instead of panics.
- Keep benchmark claims tied to a concrete host, operating system, protocol, payload, concurrency, warmup, and repetition count.
