# Configuration

[简体中文](configuration.zh-CN.md) | [Docs Index](README.md)

Configuration in Gnalloy modules is explicit. Prefer constructor arguments, option structs, and application-owned configuration files over package-level mutable state.

## Primary Configuration Points
- Configure upstream name servers, exchange timeout, cache policy, search domains, and hosts overrides according to the caller environment.
- Network transport for DNS is explicit: UDP, TCP fallback, or QUIC depending on the resolver module in use.
- QUIC and HTTP/3 paths require TLS 1.3 and a valid ALPN such as `h3`, `doq`, or the WebTransport profile in use.

## Recommended Defaults

- Start with bounded sizes and short integration-test timeouts.
- Increase limits only after measuring realistic payloads and peer behavior.
- Keep security-sensitive defaults closed or conservative.
- Document every production override in the owning service, not in this library module.

## Environment Variables

This library module does not require repository-specific environment variables for normal unit tests. Applications, examples, benchmarks, and CI jobs may define their own variables around it.

## Local Workspace Development

Use a local `go.work` file only as a developer convenience. Published module metadata should remain portable and must not contain machine-specific paths.
