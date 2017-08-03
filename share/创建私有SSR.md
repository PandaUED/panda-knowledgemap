# 创建私有SSR

![](https://o4j4l4n7h.qnssl.com/2017-08-01-103707.jpg)

- 性价比爆炸
- 装了BBR之后，翻墙基本满速

## Step 1

- 拥有个paypal账号 并绑上银行卡
- 登录 <https://www.vultr.com/> 注册一个账号

## Step 2

- 切换到 `Biling-Paypal` 页面 首冲`5刀`
- 回到 <https://my.vultr.com/> 点加号

1. Tokyo日本机房
2. CentOS
3. 7中可以给你的服务器起个名字

点`Deploy Now`购买

## Step 3

- 回到 <https://my.vultr.com/> 等待菊花结束
- 进入服务器详情，查看服务器的`IP`,`Username`和`Password`
- 打开电脑中的`Terminal`,输入

```bash
ssh root@45.76.196.81
```

>  root@后面跟你的IP地址,要写yes就打yes,要写密码就复制密码

- 首先安装 [BBR](https://www.91yun.org/archives/5174)

- 依次输入并回车

```bash
wget --no-check-certificate https://github.com/teddysun/across/raw/master/bbr.sh

chmod +x bbr.sh

./bbr.sh
```

- 看到提示，按`y`回车重启服务器, 重新登录服务器

```bash
uname -r

sysctl net.ipv4.tcp_available_congestion_control

sysctl net.ipv4.tcp_congestion_control

sysctl net.core.default_qdisc

lsmod | grep bbr
```


- 接着安装 [SSR](https://www.91yun.org/archives/2079)

```bash
wget -N --no-check-certificate https://raw.githubusercontent.com/91yun/shadowsocks_install/master/shadowsocksR.sh && bash shadowsocksR.sh
```

- 取一个密码
- 取一个端口号如：`1234`

- 下载SSR客户端<https://github.com/breakwa11/shadowsocks-rss>

- 进入服务器配置
- 地址填`ip`后面填上刚才配的端口号`1234`
- 加密方式选`chacha20`
- 密码写刚才配的
- 协议选`auth_sha1_v4`
- 混淆选`tls1.2_ticket_auth`
