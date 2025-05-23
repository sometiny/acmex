## 基于ACMEv2的SSL证书管理系统
完全私有部署，私密信息加密保存在自己设备，支持各种ACMEv2协议的SSL证书服务商。

### 一、支持功能
* webui管理。
* `Let's encrypt`/`Google`/`ZeroSSL`/`BuyPass`/`SSL.COM` 接口，Google、ZeroSSL和SSL.COM需要绑定EAB信息。[EAB指引](https://bkssl.com/document/acmev2-eab.html)。
* `阿里云`/`腾讯云`/`Cloudflare`/`DNS.COM`/`DNS.LA`/`百度云` DNS解析接口。
* 自定义DNS解析接口。
* SSL证书一键部署(本地/FTP/SSH/宝塔/IIS)
* SSL证书多目标部署
* 可纯前端生成CSR和私钥，降低私钥在网络上暴露的风险。
* 支持Socks5代理设置。
* 支持证书申请结果回调，可自行部署证书。
* windows/osx/linux多平台部署。
* docker容器运行。
* 系统服务运行。
* 远程目录列出(本地/FTP/SSH/宝塔/IIS)。
* 域名有效性验证。
* 对DNS-01和HTTP-01的预验证。
* 一键导入宝塔站点。
* DNS-01验证的CNAME模式并对CNAME进行预验证。
* 自动续期。
* 自定义ACME服务商。
* 邮件通知。

### 二、安装运行

#### 1、下载
从[https://github.com/sometiny/acmex/releases/latest](https://github.com/sometiny/acmex/releases/latest)选择下载合适的release。


#### 2、设置
运行命令，设置webui管理地址。

```bash
./acmex setup --listen-at "127.0.0.1:1084"
# 127.0.0.1:1084 监听本地回环地址1084端口，webui仅限本机访问
# 0.0.0.0:1084 监听所有本机所有ip的1084端口，webui服务会暴露到公网访问
# 可自定义端口
```

#### 3、启动webui
有两种方式可以启动webui，任选一种即可。
##### 使用控制台启动。
适合临时启动或docker运行
```bash
./acmex --runas console
```
##### 安装为系统服务
适合长期提供webui服务
```bash
./acmex --install-as [服务名称]
```

#### 4、访问webui
服务启动后，浏览器访问 `http://127.0.0.1:端口` 即可打开管理面板。

具体访问地址根据setup时设置的监听地址有关。

#### 5、使用docker安装和运行
以`alpine`为例，使用alpine镜像运行acmex。

从`https://github.com/sometiny/acmex/releases/latest`下载`acmex-linux-musl-x64.zip`，解压后将acmex复制到本地系统，例如：`/home/acmex/linux-musl-x64/acmex`。

##### 设置acmex
使用alpine运行docker，设置acmex初始参数。

映射发行版所在目录到容器的/home/acmex目录。

设置完成后容器自动删除。
```bash
docker run -it --rm \
-e "WITH_DOCKER=yes" \
-v /home/acmex/linux-musl-x64:/home/acmex \
alpine \
/home/acmex/acmex setup --listen-at 0.0.0.0:80
```

##### 启动acmex

设置端口映射：127.0.0.1:1084 => 容器的80端口。

设置自动重启，内存限制512m。

使用--runas console启动acmex。
```bash
docker run -id --name alpine-acmex --restart always -m 512m \
-p 127.0.0.1:1084:80 \
-v /home/acmex/linux-musl-x64:/home/acmex \
alpine \
/home/acmex/acmex --runas console
```
Docker启动后，浏览器访问 `http://127.0.0.1:1084` 即可打开管理面板。


### 四、业务流程
* webui选择合适的算法、填写要签发的域名，系统自动生成CSR，并将私钥返回，私钥需要自行妥善保存（建议使用纯JS或自行提供CSR，降低私钥在网络上的暴露风险）。
* 系统向SSL证书服务商发起签发请求。
* 服务商会要求进行域名验证，DNS/HTTP等方式。
* DNS解析完成或http文件部署成功后，系统向服务商发起验证请求。
* 服务商域名验证通过后，系统向服务商发起颁发请求，服务商返回已颁发的证书。
* 可以选择通过webui将证书部署到指定的目标，系统支持通过FTP/SSH/宝塔/IIS等来部署。


DNS解析可以选择手动解析，也可以在webui配置相关接口后，一键解析。

通过webui部署SSL证书时，需要设置相关的部署目标信息。