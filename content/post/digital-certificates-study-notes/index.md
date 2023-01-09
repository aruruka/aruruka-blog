---
title: Digital Certificates Study Notes
subtitle: digital certificate, asymmetric encryption, public key encryption,
  HTTPS, TLS, diagramming
date: 2023-01-09T10:31:11.415Z
summary: >-
  Today I answered a question on Quora: **How are API keys and secret keys
  different from public and private key encryption?**


  I found some good articles that can be used as a quick reference. These articles introduce enough information about TLS, HTTPS, asymmetric encryption. They are useful when you need to sort out the meaning of those many components.
draft: false
featured: false
authors:
  - Raymond Yan
tags:
  - tls
  - https
  - asymmetric encryption
  - public key encryption
  - digital certificate
categories:
  - networking
  - security
image:
  filename: ""
  focal_point: Smart
  preview_only: false
---
Today I answered a question on Quora: **How are API keys and secret keys different from public and private key encryption?**

This is the answer I wrote: <https://qr.ae/prs1J7>

The reason I came across this question is that I was learning Python programming, and I came across an example of a RESTful HTTP POST request, the code is as follows.

A﻿n example of HTTP request calling Gemini API to make an order. 👇

```python
import requests
import json
import base64
import hmac
import hashlib
import datetime
import time

base_url = "https://api.sandbox.gemini.com"
endpoint = "/v1/order/new"
url = base_url + endpoint

gemini_api_key = "account-zmidXEwP72yLSSybXVvn"
gemini_api_secret = "375b97HfE7E4tL8YaP3SJ239Pky9".encode()

t = datetime.datetime.now()
# print(t)
payload_nonce = str(int(time.mktime(t.timetuple())*1000))

payload = {
    "request": "/v1/order/new",
    "nonce": payload_nonce,
    "symbol": "btcusd",
    "amount": "5",
    "price": "3633.00",
    "side": "buy",
    "type": "exchange limit",
    "options": ["maker-or-cancel"]
}

encoded_payload = json.dumps(payload).encode()
b64 = base64.b64encode(encoded_payload)
signature = hmac.new(gemini_api_secret, b64, hashlib.sha384).hexdigest()

request_headers = {
    'Content-Type': "text/plain",
    'Content-Length': "0",
    'X-GEMINI-APIKEY': gemini_api_key,
    'X-GEMINI-PAYLOAD': b64,
    'X-GEMINI-SIGNATURE': signature,
    'Cache-Control': "no-cache"
}

response = requests.post(url,
                         data=None,
                         headers=request_headers)

new_order = response.json()
print(new_order)
```

Some of these operations encrypt the content of the request.
I haven't really understood the principles of technologies such as TLS, HTTPS, and public-private key, so I want to know more details.

I found this article 🔗[数字签名是什么？](https://www.ruanyifeng.com/blog/2011/08/what_is_a_digital_signature.html) written by Ruan YiFeng, to be precise, he translated it.

The English original URL of the original author (David Youd) is 🔗here: [What is a Digital Signature?](http://www.youdzone.com/signature.html)

This article is really, really good! It explains enough information with a very effective and easy to understand example, combined with pictures. This article can be used as a quick reference manual, and you can quickly refer to this article when you need to sort out the various components in TLS, HTTPS, and asymmetric encryption.

I also found an article by CloudFlare on how HTTPS and asymmetric encryption work. These articles are also short, but well-organized, and are also very suitable as manuals for quick reference.

* [什么是非对称加密？](https://www.cloudflare.com/zh-cn/learning/ssl/what-is-asymmetric-encryption/)
* [TLS 握手期间会发生什么？](https://www.cloudflare.com/zh-cn/learning/ssl/what-happens-in-a-tls-handshake/)