---
title: HTTP digest authentication
subtitle: 简要介绍 HTTP digest authentication.

# Summary for listings and search engines
summary: 简要介绍 HTTP digest authentication.

# Link this post with a project
projects: []

# Date published
date: "2021-12-13T00:00:00Z"

# Date updated
lastmod: "2021-12-13T00:00:00Z"

# Is this an unpublished draft?
draft: false

# Show this page in the Featured widget?
featured: false

toc: true

pager: true

show_related: true

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
image:
  caption: "Image credit: [**Unsplash**](https://unsplash.com/photos/CpkOjOcXdUY)"
  focal_point: ""
  placement: 2
  preview_only: false

authors:
  - admin

tags:
  - Go
  - 开源

categories:
  - 教程
---

## 概述

摘要式访问身份验证（`HTTP digest authentication`）是 `Web` 服务器可用于与用户的 `Web` 浏览器协商凭据（如用户名或密码）的商定方法之一。这可用于在发送敏感信息（例如网上银行交易历史记录）之前确认用户的身份。它在通过网络发送用户名和密码之前对用户名和密码应用哈希函数。
相比之下，基本访问身份验证（`HTTP basic authentication`）使用易于逆的 `Base64` 编码而不是哈希，因此除非与 `TLS` 结合使用，否则不安全。

摘要访问身份验证最初由 `RFC 2069`[^1]（HTTP 的扩展：摘要访问身份验证）指定。`RFC 2069` 大致指定了传统的摘要式身份验证方案，其安全性由服务器生成的随机数值维护。身份验证响应的形成方式如下（其中 HA1 和 HA2 是字符串变量的名称）：

```bash
HA1 = MD5(username:realm:password)
HA2 = MD5(method:digestURI)
response = MD5(HA1:nonce:HA2)
```

`RFC 2069` 后来被 `RFC 2617`[^2]（HTTP 身份验证：基本和摘要访问身份验证）取代。`RFC 2617` 为摘要式身份验证引入了许多可选的安全增强功能;“保护质量”（Qop）、由客户端递增的随机数计数器以及客户端生成的随机随机数。这些增强功能旨在防止例如选择的明文攻击密码分析。

```bash
# HA1部分
# 当algorithm值为"MD5"或未指定时，HA1计算方法如下
HA1 = MD5(username:realm:password)
# 当algorithm值为"MD5-sess"时，HA1计算方法如下
HA1 = MD5(MD5(username:realm:password):nonce:cnonce)

# HA2部分
# 当qop值为"auth"或未指定时，HA2计算方法如下
HA2 = MD5(method:uri)
# 当qop值为"auth-int"时，HA2计算方法如下；entityBody是指整个body（？）
HA2 = MD5(method:uri:MD5(entityBody))

# response部分
# 当qop值为"auth"或"auth-int"时，response计算方法如下
response = MD5(HA1:nonce:nonceCount:cnonce:qop:HA2)
# 当qop未指定时，response计算方法如下
response = MD5(HA1:nonce:HA2)
```

名词释义：

- `username`：系统用户名；客户端自行填充
- `realm`：领域；服务端通过 `WWW-Authenticate` 头返回内容可以自己随便定，但其目的是用于提示客户端当前是什么系统，所以规范来说应类似于“myhost@testrealm.com”的形式。
- `nonce`：服务端通过 `WWW-Authenticate` 头返回的随机数
- `uri`：请求接口或资源（似乎规范来说应用 `GET` 或 `POST` 后的一样，上边例子中少了 `/` 是因为服务端没按规范实现）
- `algorithm`：后边 `response` 用的计算方法
- `cnonce`：`client nonce`，客户端生成的随机数
- `nc`：`nonce count`，用于标识进行请求的次数。
- `qop`：`quality of protection`，进一步限定 `response` 的计算方法，服务端通过 `WWW-Authenticate` 头返回。
- `response`：认证最主要的值，前面各字段除 `algorithm` 外全要参与该值的计算。

Digest 认证示例 [^3]：

```bash
GET /GetDeviceInfo HTTP/1.1
Host: 192.168.220.128
User-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64; rv:60.0) Gecko/20100101 Firefox/60.0
Authorization: Digest username="admin",realm="TVT API Test Tool",nonce="d4f95e85dc5a39a4914db61b67878f5b",uri="GetDeviceInfo",algorithm="MD5",cnonce="d4f95e85dc5a39a4914db61b67878f5b",nc=00000001,qop="auth",response="1cc4cf126d3c4a70d2de34c5d8c2943c"
Accept-Encoding: gzip, deflate
Accept: */*
Cache-Control: no-cache
Cookie: Secure
Connection: close
```

## 代码计算 Signature

```python
import hashlib

def md5(s):
    hl = hashlib.md5()
    hl.update(s.encode(encoding='utf-8'))
    return hl.hexdigest()

user = 'test'
realm = 'admin@test'
passwd = 'test'
method = 'POST'
uri = '/test/url'
nonce = 'NdtJ4sLeSvL7VOxE'
cnonce = 'd9fc4be707e5c20ea175b34641d71106'
nc = '00000001'
qop = 'auth'
ha1 = md5(":".join((user, realm, passwd)))
ha2 = md5(":".join((method, uri)))
response = md5(":".join((ha1, nonce, nc, cnonce, qop, ha2)))
print(response)

```

[^1]: https://www.ietf.org/rfc/rfc2069.txt
[^2]: https://www.ietf.org/rfc/rfc2617.txt
[^3]: https://www.cnblogs.com/lsdb/p/10621940.html
