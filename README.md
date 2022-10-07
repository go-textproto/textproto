# Golang's net/textproto but 𝙁/𝘼/𝙎/𝙏/𝙀/𝙍

## `import "gopkg.in/textproto.v0"`

![Go Import](https://img.shields.io/badge/import-gopkg.in/textproto.v0-9cf?logo=go&style=for-the-badge)
[![Go Reference](https://img.shields.io/badge/reference-go.dev-007d9c?logo=go&style=for-the-badge)](https://pkg.go.dev/gopkg.in/textproto.v0)

The Golang standard library `net/textproto` suffers in data throughput performance when using its `DotReader` or `DotWriter` implementations. It's caused by iterating each input output byte using the `ReadByte` or `WriteByte` functions. This increases a lot of CPU cycles for accessing memory for each byte. This module aim to provide an optimized implementation by leveraging the SIMD optimized `ReadSlice` and `IndexByte` functions. Here are the resulting numbers:

```
BenchmarkDotReader/Legacy-12                  62          21610894 ns/op         194.08 MB/s
BenchmarkDotReader/Optimized-12             1486            821764 ns/op        5104.02 MB/s
BenchmarkDotWriter/Legacy-12                  56          19386652 ns/op         216.35 MB/s
BenchmarkDotWriter/Optimized-12             1694            700181 ns/op        5990.31 MB/s
```
