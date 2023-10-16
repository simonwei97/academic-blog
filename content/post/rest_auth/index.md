---
title: RESTful Authentication (JWT token)
subtitle: 简要介绍 RESTful Authentication.

# Summary for listings and search engines
summary: 简要介绍 RESTful Authentication

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

当前，访问对象存储服务时，可通过 `RESTful API` 对 `S3` 发起 `HTTP` 匿名请求或者 `HTTP` 签名请求，`S3` 服务端将会对请求发起者进行身份验证。

对于签名方式，一般都是是使用 `Authorization` 进行资源访问，参考 `AWS S3` `Authorization` 请求标头结构的伪代码 [^1]：

```bash
Authorization = "AWS" + " " + AWSAccessKeyId + ":" + Signature;

Signature = Base64( HMAC-SHA1( UTF-8-Encoding-Of(YourSecretAccessKey), UTF-8-Encoding-Of( StringToSign ) ) );

StringToSign = HTTP-Verb + "\n" +
	Content-MD5 + "\n" +
	Content-Type + "\n" +
	Date + "\n" +
	CanonicalizedAmzHeaders +
	CanonicalizedResource;

CanonicalizedResource = [ "/" + Bucket ] +
	<HTTP-Request-URI, from the protocol name up to the query string> +
	[ subresource, if present. For example "?acl", "?location", or "?logging"];

CanonicalizedAmzHeaders = <described below>
```

`HMAC-SHA1` 是由 `RFC 2104` [^2]（用于消息身份验证的哈希密钥）定义的算法。

- `YourSecretKey`: 您的 `SecretKey`
- `HTTP-Verb`: 请求的方法，如：`PUT`，`GET`，`DELETE`，`POST`
- `Content-MD5`: 请求头 `Content-MD5` 的内容，如果没有这个头，由空字符串代替
- `Content-Type`: 请求头 `Content-Type` 的内容，如果没有这个头，由空字符串代替
- `Date|Expires`: 如果使用 `Authorization` 头携带签名信息，为 `Date` 头的内容，如果没有 `Date` 头，由空字符串代替；如果使用请求参数携带签名信息，为参数 `Expires` 的内容
- `CanonicalizedAmzHeaders`: 请求中所有以 `x-amz-`开始的头所组成的字符串,如果没有这样的头，由空字符串代替
- `CanonicalizedResource`: 请求所对应的资源

## canonicalizedResource 取值示例

一般 的结构如下

```bash
/[BucketName/[ObjectKey[?SubResource]]]
```

以下为示例

```bash
GET /?foo=bar
GET /bucket/key?foo=bar
GET /bucket/key?aaa&foo=bar

```

对应的 canonicalizedResource

```bash
／
/bucket/key
/bucket/key?aaa
```

## Go 代码计算 Signature

```go
package main

import (
    "crypto/hmac"
    "crypto/sha1"
    "encoding/base64"
    "fmt"
    "net/url"
    "time"
)

func main() {
    accessKey := "AKIAIOSFODNN7EXAMPLE"
    secretKey := "wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY"

    expires := time.Now().Unix() + 7200

    signatureStr := getSignature(secretKey, expires)

    fmt.Printf("signature=%s&expires=%d&access_key=%s\n", signatureStr, expires, accessKey)
}

/*
Signature = URL-Encode( Base64( HMAC-SHA1( YourSecretAccessKey, UTF-8-Encoding-Of( StringToSign ) ) ) );
*/
func getSignature(secretKey string, expires int64) string {
    httpVerb := "GET"

    canonicalizedResource := ""

    stringToSign := getStringToSign(httpVerb, canonicalizedResource, expires)
    fmt.Println("--------------------------")
    fmt.Println("stringToSign", stringToSign)
    fmt.Println("--------------------------")
    signatureStr := url.QueryEscape(Hmac(secretKey, stringToSign))
    return signatureStr
}

func Hmac(key, data string) string {
    keyByte := []byte(key)
    mac := hmac.New(sha1.New, keyByte)
    mac.Write([]byte(data))

    return base64.URLEncoding.EncodeToString(mac.Sum(nil))
}

/*
StringToSign = HTTP-VERB + "\n" +
        Content-MD5 + "\n" +
        Content-Type + "\n" +
        Expires + "\n" +
        CanonicalizedAmzHeaders +
        CanonicalizedResource;
*/

// getStringToSign
func getStringToSign(httpVerb, canonicalizedResource string, expires int64) string {
    contentMd5 := ""
    contentType := ""
    canonicalizedAmzHeaders := ""

    stringToSign := fmt.Sprintf("%s\n%s\n%s\n%d\n%s%s", httpVerb, contentMd5, contentType, expires, canonicalizedAmzHeaders, canonicalizedResource)

    return stringToSign
}
```

## Python 代码计算 Signature

```python
import hashlib
import hmac
import time
import binascii

# 验证信息
AK = 'AKIAIOSFODNN7EXAMPLE'
SK = 'wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY'


# 指定HTTP方法，可选GET/PUT/DELETE/POST/OPTIONS
httpMethod = "GET"

# 指定请求的Header:Content-Type和Content-MD5
contentType = ""
contenMD5 = ""

expires = int(time.time()) + 7200
print("expries", int(time.time()))

# 填写canonicalizedHeaders
canonicalizedHeaders = ""

# 填写CanonicalizedResource
CanonicalizedResource = ""

# 生成StringToSign
canonical_string = httpMethod + "\n" + contenMD5 + "\n" + contentType + "\n" + str(expires) + "\n" + canonicalizedHeaders + CanonicalizedResource

# 打印StringToSign以便出现问题时进行验证
print("------------------------------")
print("signToString", canonical_string)
print("------------------------------")
# 计算签名并进行BASE64编码
hashed = hmac.new(SK.encode('UTF-8'), canonical_string.encode('UTF-8'), hashlib.sha1)
encode_canonical = binascii.b2a_base64(hashed.digest())[:-1].decode('UTF-8')

# 打印
print("signature={0}&expires={1}&access_key={2}".format(encode_canonical,expires, AK))
```

## 参考

[^1]: https://docs.aws.amazon.com/zh_cn/AmazonS3/latest/userguide/RESTAuthentication.html
[^2]: https://www.ietf.org/rfc/rfc2104.txt
[^3]: https://www.cnblogs.com/lsdb/p/10621940.html
