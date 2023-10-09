---
title: Tshark常用命令
linktitle: Tshark常用命令
type: book
date: "2022-05-05T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 2
---

```bash
# 显示Tshark的版本信息
tshark -v

# 显示Tshark的帮助信息
tshark -h

# 列出可用的网络接口
tshark -D
```

## 过滤指定端口包

要过滤 PCAP 包中指定端口的 HTTP 报文，可以使用 tshark 命令结合 BPF 过滤器来实现。以下是一个示例命令：

```bash
tshark -r <input_file> -Y "tcp.port == <port_number> and http"
```

其中， `<input_file>` 是要读取的 `PCAP` 文件路径，` <port_number>` 是要过滤的端口号。

这个命令使用了 `-r` 选项指定要读取的 `PCAP` 文件， `-Y` 选项后面跟着 `BPF` 过滤器表达式。 `tcp.port == <port_number>` 表示过滤指定端口的 `TCP` 流量， `http` 表示只显示 `HTTP` 协议的报文。

运行命令后，tshark 将只显示指定端口的 `HTTP` 报文，你可以根据需要进行进一步的分析或处理。
