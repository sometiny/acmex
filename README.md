
## 带webui的免费SSL证书管理工具


### 一、功能
* 内置 `Let's encrypt`/`Google`/`ZeroSSL` 接口，Google和ZeroSSL需要绑定EAB信息。[EAB指引](https://bkssl.com/document/acmev2-eab.html)。
* 内置 `阿里云`/`腾讯云`/`Cloudflare`/`DNS.COM`/`DNS.LA`/`百度云` DNS解析接口。
* 支持自定义DNS解析接口。
* 支持一键部署(本地/FTP/SSH/宝塔/IIS)
* 可纯前端生成CSR和私钥，降低私钥在网络上暴露的风险。
* 支持Socks5代理设置。
* 支持证书申请结果回调，可自行部署证书。
* 支持windows/osx/linux运行
* 支持docker容器运行
* 支持以系统服务运行

### 二、运行

#### 1、下载
从[https://github.com/sometiny/acmex/releases](https://github.com/sometiny/acmex/releases)下载最新的release：acmex.zip

#### 2、根据系统发行版选择合适的二进制文件
运行命令，设置webui管理地址。

```bash
./acmex setup --listen-at "127.0.0.1:1084"
# 127.0.0.1:1084 监听本地回环地址1084端口，webui仅限本机访问
# 0.0.0.0:1084 监听所有本机所有ip的1084端口，webui服务会暴露到公网访问
# 可自定义端口
```

#### 3、启动webui
设置成功后，使用控制台命令可直接启动webui。
```bash
./acmex --runas console
```
也可以使用命令安装为系统服务
```bash
./acmex --install-as [服务名称]
```

#### 4、访问webui
服务启动后，浏览器访问 `http://127.0.0.1:端口` 即可打开管理面板。

具体访问地址根据setup时设置的监听地址有关。


### 三、业务流程
* webui选择合适的算法、填写要签发的域名，系统自动生成CSR，并将私钥返回，私钥需要自行妥善保存（建议使用纯JS或自行提供CSR，降低私钥在网络上的暴露风险）。
* 系统向SSL证书服务商发起签发请求。
* 服务商会要求进行域名验证，DNS/HTTP等方式。
* DNS解析完成或http文件部署成功后，系统向服务商发起验证请求。
* 服务商域名验证通过后，系统向服务商发起颁发请求，服务商返回已颁发的证书。
* 可以选择通过webui将证书部署到指定的目标，系统支持通过FTP/SSH/宝塔/IIS等来部署。


DNS解析可以选择手动解析，也可以在webui配置相关接口后，一键解析。

通过webui部署SSH证书时，需要设置相关的部署目标信息。