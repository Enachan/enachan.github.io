---
date: 2017-02-09 18:11:53 +0800
title: Python设置HTTP代理通过Charles抓包
layout: post
permalink: /post/python-and-charles-http-proxy.html
hljs: true
---

平常在开发接口过程中，下断点调试或者直接打印太麻烦，偶尔想抓一下包，Mac下有抓包神器Charles。有两种方式：

* **设置全局代理**，Proxy -> Mac OS X Proxy<br>
    由于Mac上使用了Surge，已经设置了全局代理，Charles全局代理会影响上网

* **不设置全局代理**<br>
    需在请求中指定代理

verify_path是证书地址，用于查看https请求响应包，Help -> SSL Proxying -> Save Charles Root Certificate...

```
import requests

def test():
    verify_path = "/Users/Enachan/Documents/charles-ssl-proxying-certificate.pem"
    # proxy会覆盖全局代理，如果只指定了http代理，会自动填上已设置的全局https代理
    proxy = {
        'http': "http://192.168.100.66:8880",
        'https': "http://192.168.100.66:8880",
    }

    # 1.全局代理
    req = requests.get("https://api.github.com/", verify=verify_path)

    # 2.非全局代理
    req = requests.get("https://api.github.com/", proxies=proxy, verify=verify_path)

```

#### 参考

* [Charles Documentation](https://www.charlesproxy.com/documentation/)
* [Charles从入门到精通](http://blog.devtang.com/2015/11/14/charles-introduction/)


