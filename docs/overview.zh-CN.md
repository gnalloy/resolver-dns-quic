# 概览

[English](overview.md) | [文档索引](README.zh-CN.md)

## 目标

Gnalloy resolver 的 DNS-over-QUIC exchanger，基于 RFC 9250 ALPN doq 与 QUIC stream。

该模块提供名称解析构件，供上层 transport 和 client 使用。DNS 消息解析、交换策略、超时和缓存边界保持显式。

## 仓库身份

- 模块路径：`gnalloy.org/resolver-dns-quic`
- GitHub 仓库：`github.com/gnalloy/resolver-dns-quic`
- 默认分支：`dev`
- 许可证：Apache-2.0

## 包结构
- `gnalloy.org/resolver-dns-quic`（`quic`）

## 直接 Gnalloy 依赖

- `gnalloy.org/codec-dns`
- `gnalloy.org/resolver-dns`
- `gnalloy.org/transport-quic`

## 当前仓库集合中的直接下游

- `gnalloy.org/examples`

## 架构位置

Gnalloy 保持核心小而轻依赖。本仓库围绕单一职责形成可替换模块，通过显式 Go package 连接，而不是依靠运行时发现。

## 兼容性

公共导入路径是 `gnalloy.org/resolver-dns-quic`。首个稳定 tag 发布前，请按依赖策略使用 `@dev` 或明确的 pseudo-version。
