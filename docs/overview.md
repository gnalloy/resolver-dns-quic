# Overview

[简体中文](overview.zh-CN.md) | [Docs Index](README.md)

## Purpose

DNS-over-QUIC exchanger for Gnalloy resolver using RFC 9250 ALPN doq over QUIC streams.

This module provides name-resolution building blocks for higher-level transports and clients. It keeps DNS message parsing, exchange policy, timeout, and cache concerns explicit.

## Repository Identity

- Module path: `gnalloy.org/resolver-dns-quic`
- GitHub repository: `github.com/gnalloy/resolver-dns-quic`
- Default branch: `dev`
- License: Apache-2.0

## Package Map
- `gnalloy.org/resolver-dns-quic` (`quic`)

## Direct Gnalloy Dependencies
- `gnalloy.org/codec-dns`
- `gnalloy.org/resolver-dns`
- `gnalloy.org/transport-quic`

## Direct Dependents in the Current Module Plan
- `gnalloy.org/examples`

## Architecture Position

Gnalloy keeps the core small and dependency-light. This repository is a replaceable module around one responsibility, connected through explicit Go packages instead of runtime discovery.

## Compatibility

The public import path is `gnalloy.org/resolver-dns-quic`. Until the first stable tag is published, use `@dev` or an explicit pseudo-version selected by your dependency policy.
