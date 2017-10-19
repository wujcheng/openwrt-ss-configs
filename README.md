# openwrt-ss-configs

本项目是基于ar71xx平台无线路由器，运行OpenWrt 15.05.1后，运行Shadowsocks-libev的高级配置，支持远程加密的配置文件更新。

你可以通过以下方式，进行小额捐赠，以表达对项目发起者的感谢：

- 支付宝：`laxers@gmail.com`（请以留言的方式，告诉译者你想说的话）
- Bitcoin: `1Dh1b7DSZc9myZDdWtQte6e35FDHwHrDWa`

2017-10-19

- 将 `wan_mac_bind`与`decide_whether_subscribed`移入到`/usr/bin/update-actions`，解决脚本报错问题

2017-10-8

- 将有关shadowsocks的更新脚本从`/usr/bin/update-actions`中分离出来，形成独立的`/usr/bin/setup`
- 引入配置文件`/etc/openwrt_ss.conf`，保存一些配置; 同时引入了读写配置文件的sh库-`/usr/bin/config.shlib`
- 加入付费才开通功能，主要是通过随机化WAN mac地址，并将随机后的地址持久化，放入到一个列表中，随后将机器的mac地址与该列表匹配，根据匹配结果决定是否开通功能
- 更新`libmbedtls`到`2.5.1`，`shadowsocks-libev`到`3.1.0`

2017-1-5
- 通过改进`/etc/init.d/shadowsocks`，实现对`servers.conf`的随机化处理，得到`/etc/servers.used`独特文件，保证不同路由器上的`serverList`配置不一样，以提高DNS查询及连接速度的提升。

- 通过[`/etc/servers.conf`](https://github.com/gnu4cn/openwrt-ss-configs/blob/master/shadowsocks/etc/servers.conf)文件，及[`/etc/init.d/shadowsocks`](https://github.com/gnu4cn/openwrt-ss-configs/blob/master/shadowsocks/etc/init.d/shadowsocks), 配合[`/usr/bin/shadowsocks-firewall`](https://github.com/gnu4cn/openwrt-ss-configs/blob/master/shadowsocks/usr/bin/shadowsocks-firewall), 实现多线路并发负载均衡。
- 导入私钥，实现`/etc/servers.conf`加密传输(使用GnuPG)。
- 经由反向SSH Tunnel，实现远程管理。
- 通过[`/usr/bin/update`](https://github.com/gnu4cn/openwrt-ss-configs/blob/master/shadowsocks/usr/bin/update)实现配置文件远程更新，用于投送新的`/etc/servers.conf`配置及错误修正。

如你打算采用本项目方案，请生成自己的gpg密钥，将私钥导入无线路由器，并对一些配置进行调整，即可使用。

# [XFOSS.COM](https://xfoss.com/)
