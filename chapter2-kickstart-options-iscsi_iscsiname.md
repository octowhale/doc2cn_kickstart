## iscsi 


在安装过程中添加额外的iSCSI存储。如果使用了iscsi参数，则必须使用iscsiname参数为iSCSI节点指定一个名字。且在KickstartFile文件中，iscsiname参数必须出现在在iscsi参数的前面。

 iscsi --ipaddr= [options] 

我们建议在系统中BIOS或者固件(Intel体系中的iBFT)中，任何能配置iSCSI存储地方进行配置，而不是使用iscsi参数。Anaconda自动发现和使用在BIOS或固件中配置过的磁盘，而不需要在KickstartFile文件中额外配置。
如果必须使用iscsi参数，确保在安装开始时，网络可以正常使用，且在KickstarFile文件中iscsi参数出现的位置在调用iSCSI磁盘的参数之前，比如说clearpart或ignoredisk

  + --ipaddr= (必填项(mandatory))
    + 连接目标的IP
  + --port
    + 连接目标时使用的端口号(默认值：--port=3260)
  + --target
    + 目标iqn
  + --iface
    + 将连接绑定到分配网络接口，而不是使用网络层分配的默认接口。一旦使用，必须分配给所有iscsi命令。
  + --user
    + 可以访问目标的用户名
  + --reverse-user
    + 使用反向CHAP身份认证的目标端对应的发起端(initiator)鉴定所使用的用户名。
  + --reverse-password
    + 发起端指定的用户对应的密码



## iscsiname 


为计算机分配一个发起端名。如果在KickstartFile中使用了iscsi参数，那么此参数是必需的。在KickstartFile中，iscsiname必出出现在iscsi之前。

