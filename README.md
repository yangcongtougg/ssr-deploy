# ssr-deploy
>以下为ssr的构建步骤，推荐使用Debian GNU/Linux 8(jessie)


- 进入linux系统，切换到root路径 sudo-i。
- 安装基于google的TCP-BBR拥堵算法的加速器，相较于魔改版BBR,速度很惊人。
- 执行```wget --no-check-certificate https://github.com/iyuco/scripts/raw/master/bbr.sh```。
- 然后执行```chmod +x bbr.sh```。
- 最后执行`./bbr.sh`,之后选择重启。
- 重新进入系统之后,cd到root根目录。
- 查看TCP-BBR是否安装成功。依次执行下列步骤:
- 执行`uname -r`,查看内核版本，若包含有 4.9及以上就表示 OK 了。
- 检测是否完全生效:执行`sysctl net.ipv4.tcp_available_congestion_control`,返回值若为：net.ipv4.tcp_available_congestion_control = bbr cubic reno 即可。
- 接着输入:`sysctl net.ipv4.tcp_congestion_control`,返回值一般为：net.ipv4.tcp_congestion_control = bbr。
- 接着输入:`sysctl net.core.default_qdisc`,返回值一般为：net.core.default_qdisc = fq。
- 最后再输入:`lsmod | grep bbr`,返回值有 tcp_bbr 模块即说明bbr已启动。
- 安装SSR执行```wget --no-check-certificate https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocksR.sh && chmod +x shadowsocksR.sh```。
- 然后执行```./shadowsocksR.sh```,输入ssr密码,依次选择端口号,加密协议及混淆参数,根据自己的需要进行选择。
- 为vm实例添加的http及https添加防火墙规则,tcp及udp的端口号为设置的ssr的端口号，当然你也可以不设定防火墙规则，允许所有连接接入,安全性欠佳。
- 之后就可以在服务端配置使用。

---
如果想安装BBR魔改版加速器:
``wget -N --no-check-certificate https://raw.githubusercontent.com/FunctionClub/YankeeBBR/master/bbr.sh && bash bbr.sh install``
蓝底窗口选择NO，重启即可。
