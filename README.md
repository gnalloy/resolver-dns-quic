# resolver-dns-quic

DNS-over-QUIC exchanger for Gnalloy resolver using RFC 9250 ALPN doq over QUIC streams.

This repository is part of the Gnalloy modular networking stack. The default branch is `dev`; no release tag is created during bootstrap.

## Install

```bash
go get gnalloy.org/resolver-dns-quic@dev
```

## Module Boundary

- Module path: `gnalloy.org/resolver-dns-quic`
- Responsibility: DNS-over-QUIC exchanger for Gnalloy resolver using RFC 9250 ALPN doq over QUIC streams
- Core dependency: `gnalloy.org/gnalloy` when this module uses Gnalloy buffers, channels, event loops, or bootstrap contracts.

## Gnalloy Dependencies

- `gnalloy.org/codec-dns`
- `gnalloy.org/resolver-dns`
- `gnalloy.org/transport-quic`

## Development

```bash
go test ./... -count=1
go vet ./...
go test ./... -run '^$' -bench . -benchmem -benchtime=100ms -count=1
```

For multi-repository development, use the workspace at `G:\opensource\gnalloy\go.work`. For standalone verification, set `GOWORK=off`.

## License

Apache-2.0.
