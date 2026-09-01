# Examples

[简体中文](examples.zh-CN.md) | [Docs Index](README.md)

## Example 1: Add the Module to an Application

```bash
mkdir gnalloy-app && cd gnalloy-app
go mod init example.com/gnalloy-app
go get gnalloy.org/resolver-dns-quic@dev
go doc gnalloy.org/resolver-dns-quic
```

## Example 2: Inspect Current Packages

The current source tree exposes these package import paths:
- `gnalloy.org/resolver-dns-quic`

Use `go doc` against the package that matches the behavior you need:

```bash
go doc gnalloy.org/resolver-dns-quic
```

Selected current exported entry points:
- `const DefaultALPN = "doq" ...`
- `type Exchanger struct{ ... }`

## Example 3: Use Executable Tests as Behavioral Examples

Repository tests are executable examples of supported behavior. Start with the selected names below, then read the matching `_test.go` files for complete setup and assertions. See [Testing and Performance](testing.md) for the complete discovered list.

```bash
GOWORK=off GOTOOLCHAIN=local go test ./... -run Test -count=1
```

Selected current test, benchmark, fuzz, and example entry points:
- `TestExchangerUsesDoQALPNAndLengthPrefixedStream`

## Example 4: Cross-Module Assembly

Direct Gnalloy dependencies for this module:
- `gnalloy.org/codec-dns`
- `gnalloy.org/resolver-dns`
- `gnalloy.org/transport-quic`

Assembly guidance:
- Use this resolver module where applications need DNS resolution as an explicit dependency.
- Transport and protocol choices stay visible in application configuration.
- Cache, timeout, and fallback behavior should be validated with the final network policy.

## Example 5: Pressure-Test Harness

For sustained load, wire this module into a scenario under `gnalloy.org/benchmarks` or a runnable client under `gnalloy.org/examples` when the module participates in network traffic. Record host, OS, CPU, Go version, protocol, payload, concurrency, warmup, repetitions, throughput, and p99 latency in the report.
