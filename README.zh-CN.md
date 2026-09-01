# resolver-dns-quic

[English](README.md) | [文档](docs/README.zh-CN.md)

Gnalloy resolver 的 DNS-over-QUIC exchanger，基于 RFC 9250 ALPN doq 与 QUIC stream。

该模块提供名称解析构件，供上层 transport 和 client 使用。DNS 消息解析、交换策略、超时和缓存边界保持显式。

## 状态

- 导入路径：`gnalloy.org/resolver-dns-quic`
- 仓库：`github.com/gnalloy/resolver-dns-quic`
- 默认分支：`dev`
- 预览安装：`go get gnalloy.org/resolver-dns-quic@dev`
- 许可证：Apache-2.0

## 安装
```bash
go get gnalloy.org/resolver-dns-quic@dev
go doc gnalloy.org/resolver-dns-quic
GOWORK=off GOTOOLCHAIN=local go test ./... -count=1
```

## 文档
- [概览](docs/overview.zh-CN.md) ([English](docs/overview.md))
- [用法](docs/usage.zh-CN.md) ([English](docs/usage.md))
- [案例](docs/examples.zh-CN.md) ([English](docs/examples.md))
- [配置说明](docs/configuration.zh-CN.md) ([English](docs/configuration.md))
- [测试与性能](docs/testing.zh-CN.md) ([English](docs/testing.md))
- [API 参考](docs/api.zh-CN.md) ([English](docs/api.md))
- [注意事项与备注](docs/notes.zh-CN.md) ([English](docs/notes.md))
- [ADR-001 模块边界](docs/decisions/0001-module-boundary.zh-CN.md) ([English](docs/decisions/0001-module-boundary.md))

## 模块边界

本仓库负责：Gnalloy resolver 的 DNS-over-QUIC exchanger，基于 RFC 9250 ALPN doq 与 QUIC stream。

它不吸收相邻模块职责。核心基础能力保留在 `gnalloy.org/gnalloy`；协议 codec、transport、handler、resolver、examples 与 benchmarks 分别由独立仓库负责。

## 包结构
- `gnalloy.org/resolver-dns-quic`（`quic`）

## Gnalloy 依赖

- `gnalloy.org/codec-dns`
- `gnalloy.org/resolver-dns`
- `gnalloy.org/transport-quic`

## 常见集成方式
- 根据调用方环境配置上游 nameserver、交换超时、缓存策略、search domain 与 hosts override。
- DNS 网络传输是显式的：根据使用的 resolver 模块选择 UDP、TCP fallback 或 QUIC。
- QUIC 与 HTTP/3 路径要求 TLS 1.3，并使用有效 ALPN，例如 `h3`、`doq` 或 WebTransport 使用的 profile。

## 当前公共入口

生成的 API 参考列出了完整公共面。当前常用构造函数或 option 类型包括：
- `const DefaultALPN = "doq" ...`

## 验证

```bash
GOWORK=off GOTOOLCHAIN=local go test ./... -count=1
GOWORK=off GOTOOLCHAIN=local go vet ./...
GOWORK=off GOTOOLCHAIN=local go test ./... -run '^$' -bench . -benchmem -count=1
```

压测时，将该模块和相应 transport、codec、handler 栈装配后，使用 `gnalloy.org/benchmarks` 或 `gnalloy.org/examples` 中的场景运行。报告必须保留主机、操作系统、payload、并发度、warmup 和 repetition。

## 注意事项
- 本仓库保持窄边界。跨模块行为应在应用、recipes、examples 或 benchmark harness 中装配。
- 公共 API 必须保持 Go 原生和显式；热路径避免运行时扫描、隐藏全局注册表和重反射。
- 网络输入一律视为不可信。配置解析上限，返回类型化错误，不使用 panic 处理输入错误。
- 性能结论必须绑定具体主机、操作系统、协议、payload、并发度、warmup 和 repetition。
