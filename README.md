```bash
#1、启动为控制台项目
sudo ./acmex --runas console

#2、安装为系统服务
sudo ./acmex --install-as [服务名称]
```
首次运行需要设置管理面板监听地址。

* 1、仅本机访问管理面板，监听：`127.0.0.1:端口`
* 2、允许公网访问，监听：`0.0.0.0:端口`，允许公网访问时，注意安全策略。

服务启动后，浏览器访问 `http://127.0.0.1:端口` 即可打开管理面板。

* 内置 `Let's encrypt`/`Google`/`ZeroSSL` 接口。
* 内置 `阿里云`/`腾讯云`/`Cloudflare` DNS解析接口。
* 支持 自定义 DNS解析接口。
* 可纯前端生成CSR和私钥，降低私钥在网络上暴露的风险。
* 支持Socks5代理设置。
* Google和ZeroSSL需要绑定EAB信息。[EAB指引](https://bkssl.com/document/acmev2-eab.html)