```bash
#启动为控制台项目
./acmex --runas console

#安装为系统服务
./acmex --install-as [acmex]
```
首次运行需要设置控制面板监听的地址。

* 1、仅本机访问控制面板，监听：`127.0.0.1:端口`
* 2、允许公网访问，监听：`0.0.0.0:端口`，允许公网访问时，注意安全策略。

服务启动后，浏览器访问 `http://127.0.0.1:端口` 即可打开控制面板。

* 内置了 `Let's encrypt`/`Google`/`ZeroSSL` 的免费接口。
* 内置了 `阿里云`/`腾讯云`/`Cloudflare` 的DNS接口。
* 可纯前端生成CSR和私钥，降低私钥在网络上暴露的风险。
* 支持Socks5代理设置。
* Google和ZeroSSL需要绑定EAB信息。[Google EAB指引](https://wos.cc/document/google-ssl.html)