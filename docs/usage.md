# Usage

[简体中文](usage.zh-CN.md) | [Docs Index](README.md)

## Requirements

- Go 1.25 or newer, matching the module `go` directive.
- A Gnalloy application, recipe, example, or benchmark harness that owns lifecycle and deployment configuration.
- Standalone module verification should set `GOWORK=off` so the module is tested through its published dependency graph.

## Install
```bash
go get gnalloy.org/resolver-dns-quic@dev
```

## Import
```go
import "gnalloy.org/resolver-dns-quic"
```

## Integration Pattern
- Configure upstream name servers, exchange timeout, cache policy, search domains, and hosts overrides according to the caller environment.
- Network transport for DNS is explicit: UDP, TCP fallback, or QUIC depending on the resolver module in use.
- QUIC and HTTP/3 paths require TLS 1.3 and a valid ALPN such as `h3`, `doq`, or the WebTransport profile in use.

## API Selection

Use the API inventory to choose the exact constructor or option type for your protocol path:

```bash
go doc gnalloy.org/resolver-dns-quic
```

Common current entry points:
- `const DefaultALPN = "doq" ...`

## Cross-Module Assembly

When multiple Gnalloy repositories are developed together, create a local `go.work` file in your chosen workspace. Keep application-local `replace` directives out of published library modules unless the change is intentionally temporary and never committed.

## Error Handling

Network input, peer behavior, platform capability, and timeout failures must be handled as normal errors. Do not recover protocol correctness by panicking. Return or propagate the module error and close the affected Channel when ownership requires it.
