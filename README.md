
### 带webui的免费SSL证书管理工具

项目地址：[https://github.com/sometiny/acmex](https://github.com/sometiny/acmex)

```bash
#1、启动为控制台项目
./acmex --runas console

#使用-q参数，监听随机端口快速启动服务
./acmex --runas console -q

#2、安装为系统服务
./acmex --install-as [服务名称]
```
首次运行需要设置管理面板监听地址（未提供-q参数时会要求提供监听地址）。

* 1、仅本机访问管理面板，监听：`127.0.0.1:端口`
* 2、允许公网访问，监听：`0.0.0.0:端口`，允许公网访问时，注意安全策略。

服务启动后，浏览器访问 `http://127.0.0.1:端口` 即可打开管理面板。

* 内置 `Let's encrypt`/`Google`/`ZeroSSL` 接口。
* 内置 `阿里云`/`腾讯云`/`Cloudflare`/`DNS.COM`/`DNS.LA`/`百度云` DNS解析接口。
* 支持自定义DNS解析接口。
* 可纯前端生成CSR和私钥，降低私钥在网络上暴露的风险。
* 支持Socks5代理设置。
* 支持证书申请结果回调。
* Google和ZeroSSL需要绑定EAB信息。[EAB指引](https://bkssl.com/document/acmev2-eab.html)
* 支持一键部署(FTP/SSH/宝塔/IIS)
