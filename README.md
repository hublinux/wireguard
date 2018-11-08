# wireguard一键脚本
#### 适用于CentOS7
#### wireguard_install.sh 单用户版，如需增加用户需要手动增加

教程开始

1、VPS应安装为centos7系统，使用xshell或其他ssh工具连接VPS后，执行下面命令：

yum install -y wget

然后执行：

wget https://raw.githubusercontent.com/yobabyshark/wireguard/master/wireguard_install.sh && chmod +x wireguard_install.sh && ./wireguard_install.sh

2、执行脚本会弹出选择项，首先我们选择安装内核，安装过程中需要几分钟，最后按照提示重启。



3、重启完毕，使用xshell连接VPS，执行下面命令：

./wireguard_install.sh

4、执行命令会弹出和第2步相同的选择项，这次我们选择安装wireguard，安装过程中需要等几分钟，安装完成服务即自行启动了。



5、使用xftp等ftp工具连接vps，进入/etc/wireguard/目录，然后将client.conf下载到本地电脑。（这个配置文件里面包含的是客户端的各种参数，mac、linux客户端也是使用这些参数。）



6、下载安装TunSafe，这是一个windows端的第三方客户端，因为官方windows版本的还没开发完成，先用这个软件代替，TunSafe已经开源了，可以放心使用。
官网下载：https://tunsafe.com/download

7、打开TunSafe，点击file，选择import file，选择第5步下载的client.conf文件，导入到软件中。



8、导入后会自动连接，连接成功后，所有流量都会被代理，也就是全局代理。

9、使用Linux、Mac系统的同学，可以去官方查看一下如何安装对应的客户端，比较简单，这里就不讲了。

安卓版客户端教程

1、去Google Play下载wireguard，目前这个软件在Google Play中是未发布版，也可直接下载下面的f-droid的安装包。

安卓版wireguard：点击下载

2、将软件安装好，并将本教程服务端获取的client.conf文件传输到手机中。打开软件，点击加号，在弹出的页面选择create from file or archive，然后选择保存在手机的conf文件。

注意：这里可能会提示错误，原因是没有文件操作权限，去权限管理里给软件勾上存储权限即可。



选择文件后如下图所示



开启代理即可。

iOS版客户端

现在是测试版，官方提供了如何安装的步骤，贴上链接

wireguard测试版

非常重要

这里是一些大家wireguard后遇到各种问题的排查过程，遇到问题先来这里看，有遇到问题自行解决过了而且下面没提及到的，请各位童鞋留言，我会补充上。

服务端

1、首先使用 wg 命令，查看wireguard服务是否正常启动，peer是否正常。

2、检查配置文件wg0.conf，ip不可使用ipv6，因为ip是自动联网查询的，有可能会得到ipv6地址，需要改成ipv4的地址。

3、使用 ip link 命令查看物理网卡是否为eth0，如果不是将真实名称（除了lo、wg0的那个网卡）替换wg0.conf中的eth0。

4、你的云服务商的防火墙是否放行。像谷歌云/阿里云等在web控制台都可以看到防火墙设置，需自行配置放行规则。

5、你的云服务器的内网IP段不要和10.0.0.1/24冲突，我遇到过谷歌云内网网段（自己配置的）和wg使用的网段冲突的情况，这种问题很少见，除非是你自己配置的内网IP。

客户端（windows）

1、用管理员权限打开tunsafe，不要同时开启其他代理类软件。

2、如果是电脑直接拨号上网，可能会出现无法连接的情况，换路由器拨号。

3、有安装过SSTAP的情况（它安装的虚拟网卡会设置静态IP），wireguard可能会共用sstap安装的网卡，注意把这个虚拟网卡的ip和dns设置为自动获取。

4、安装过其他VPN的卸载一下，重装tunsafe试试。



关于一键脚本

1、仅适用于centos7

2、VPS架构必须是KVM

3、测试了搬瓦工、谷歌云、Vultr的centos7，可以完美搞定

4、cento7大部分内核都是3.10，不能正确安装，所以需要升级

5、有些厂商的vps内核貌似升级不了，例如vpsserver，这个还是要自行解决

关于VPS选择

如果是仅仅上外网，推荐板瓦工的年付19刀VPS，经测试在这套方案下速度也很快，秒杀ss等其他软件。


源文：
https://www.atrandys.com/2018/886.html
