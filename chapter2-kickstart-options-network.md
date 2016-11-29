## network 


为目标系统配置网络信息，并在安装器环境中激活网络设备。如果需要请求网络(如在网络安装中使用vnc)，那么设备的第一条命令应该是激活。	也可以通过--activate选项明确的指出激活设备。如果设备已经被激活(通过boot选项配置或加载UI界面)并用于获取KickstartFile文件，那么该设备会被KickstartFile文件重新激活。

在Fedora15中，激活时设备的第一条network命令，同样是为了防止非网络环境安装。但是设备不会被KickstartFile文件重新激活。

从Fedora16开始，安装器使用--activate选项可以通过kickstart网络命令配置激活的其他设备。

  + --bootproto[dhcpbootpstaticibft]
    + 默认使用DHCP。bootp和dhcp会被同等对待。
	DHCP方法是通过DHCP获取网络配置。同理，BOOTP方法是通过BOOTP服务器获取网络配置。
    + 静态(static)方法则需要在KickstartFile文件中输入所有需要的网络信息。正如方法名字，这些信息是静态的，在安装时和安装完成后都会被使用。配置静态网络命令更加麻烦，必须在命中包含所有的网络配置信息。你需要指定IP地址、子网掩码、网管、域名服务器。例如： (  表示所有信息在同一行)   

```bash


	network --bootproto=static --ip=10.0.2.15   
	--netmask=255.255.255.0 --gateway-10.0.2.254   
	--nameserver=10.0.2.1	
	

```   如果你使用静态方法，需要遵循以下限制： 所有静态网络配置信息必须卸载同一行；不能使用反斜线将多行封装成一行，比如说上面的例子。(-.-) 


	
    + ibft设置用于从iBFT表中读取配置。在Fedora16中加入。

  + --device
    + 指定需要通过network命令配置和/或激活的设备。该设备可以使用[ksdevice](http://fedoraproject.org/wiki/Anaconda_Boot_Options#ksdevice)启动选项同样的方式指定。例如：   

```bash


	network --bootproto=dhcp --device=eth0
	

```


	对于第一条网络命令，如果该选项没有被指定，那么他的默认值为1)ksdevice启动选项，2)通过kickstart激活设备，3)图形界面对话框。  对于后面的network命令，--device选项是必须的。

  + --ip
    + 网卡的IP地址。
  + --ipv6
    + 网卡的IPV6地址。可以通过格式<IPv6 address>[/prefix length>]指定，如:3ffe:ffff:0:1::1/128(如果省略掩码，则默认为64)。对于地址注册而言，auto是基于自动网络邻居发现，或"dhcp"支持DCHPv6协议。
  + --gateway
    + 默认网关，为IPv4或IPv6的地址
  + --nodefroute
    + 阻止设备抢夺默认路由。当安装器使用--activate选项激活其他设备时有用。Fedora16时加入。
  + --nameserver
    + 主要域名服务器，IP地址。多个域名服务器使用逗号分隔。
  + --nodns
    + 不配置任何DNS服务器
  + --netmask
    + 为安装完成的系统配置掩码
  + --hostname
    + 为安装完成的系统配置主机名
  + --ethtool
    + 指定额外的低等级的网络设备配置，该值将会传递给ethtool程序。
  + --essid
    + 无线网络的SSID
  + --wepkey
    + 无线网络的WEP加密秘钥
  + --wapkey
    + 无线网络的WPA加密秘钥(从Fedora16开始加入)
  + --onboot
    + 是否在启动时启用网络设备。
  + --dhcpclass
    + DHCP类别
  + --mtu
    + 网络设备的MTU大小
  + --noipv4
    + 禁用网络设备的IPv4
  + --noipv6
    + 禁用网络设备的IPv6
  + --bondslaves
    + 网卡通过--device选项命名后，可以通过该选项指定网络别名。例如：--bondslaves=eth0,eth1。Fedora19开始加入
  + --bondopts
    + 为通过--device和--bonslaves指定的网络添加一系列可选参数，使用逗号分隔。例如： --bondopts=mode=active-backup,primary=eth1。如果一个选项本身使用逗号作为分隔符，那么选项之间使用分号进行分隔。从Fedora19开始
  + --vlanid
    + 通过父设备使用--device选项来创建vlan设备的id(802.1q tag)。例如：network --device=eth0 --vlanid=171将创建vlan设备eth0.171。从Fedora19开始加入。
  + --teamslaves
    + *--device选项命名的组设备会以该选项指定的设备作为从设备。从设备之间使用逗号分隔。从设备后可以接他的配置——以单引号括起来的json格式字符串，配置中又双引号需要使用反斜线()进行转义。例如： --teamslaves="p3p1'{"prio": -10, "sticky": true}',p3p2'{"prio": 100}'"。与--teamconfig选项相同。 从Fedora20开始加入。
  + --teamconfig
    + 使用双引号将组设备配置括起来，配置使用json格式字符串，字符串中的双引号需要使用反斜线进行转义。设备名通过--device选项指定，且他的从设备和从设备的配置使用--teamslaves选项指定。从Fedora20开始加入。例如。   

```bash


	network --device team0 --activate --bootproto static --ip=10.34.102.222 --netmask=255.255.255.0 --gateway=10.34.102.254 --nameserver=10.34.39.2  
	--teamslaves="p3p1'{"prio": -10, "sticky": true}',p3p2'{"prio": 100}'" 
	--teamconfig="{"runner": {"name": "activebackup"}}"
	

```




