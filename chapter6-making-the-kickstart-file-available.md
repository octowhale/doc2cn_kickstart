# 第六章 使KickstartFile文件有效化 


KickstartFile文件必须放在以下几个位置之一：
  + 在启动磁盘上
  + 在启动CDROM上
  + 在网络位置上
通常情况下，KickstartFile文件会被复制到启动文件磁盘上，或在一个可用的网络位置。基于网络的方法是最常用的，大部分kickstart安装倾向于在网络环境中执行。
现在让我们更深入的探讨一下KickstartFile文件的位置。

## 创建一个Kickstart启动软盘 

执行一个基于软盘的kickstart安装，KickstartFile必须被命名为ks.cfg且放在软盘的根目录下。参考《RHEL安装向导》中的《创建一个软盘启动盘》章节中关于创建软盘启动的指令。由于启动盘是MS-DOS格式，因此在linux环境下，可以方便的使用mcopy命令复制ks.cfg。


```bash


mcopy ks.cfg a:


```


此外，你也可以在windows下复制该文件。你也可以在Linux下使用vfat格式挂载MS-DOS启动软盘，并用cp命令复制。

## 创建一个Kickstart启动光盘 

执行一个基于光盘的kickstart安装，KickstartFile必须被命名为ks.cfg且放在光盘的根目录下。由于CDROM是只读的，因此ks.cfg必须放在镜像的根目录下再烧录到光盘上。参考《RHEL安装向导》中的《创建一个光盘启动盘》章节中关于创建光盘启动的指定；无论如何，在创建file.iso镜像之前，需要将ks.cfg文件复制到isolinux/ 目录。

## 在网络环境创建可用KickstartFile 

使用kickstart进行网络安装非常普遍，因为系统管理员通过网络自动地为网络中的多台计算机安装系统，轻松又方便。一般而言，管理员常常在本地网络使用BOOTP/DHCP服务器和NFS服务器共同协助系统安装。BOOTP/DHCP服务器为客户机提供网络信息；NFS服务器则提供安装过程中实际使用的文件。通常，这两个服务器运行在同一台物理机上，不过也没必要一定这样。

执行一个基于网络的kickstart安装，必须在网络中运行一台BOOTP/DHCP服务器，且必须包含安装Fedora或RHEL时所用到的设备的配置信息。BOOTP/DHCP服务器提供了客户端网络信息，也指定了KickstartFile文件位置。

如果KickstartFile由BOOTP/DHCP服务器指定，那么客户端尝试通过NFS挂载文件所在目录，然后复制该文件到客户端并作为KickstartFile文件使用。

例子：一个关于DHCP服务器的dhcpd.conf片段


```bash


filename "/usr/new-machine/kickstart/";
server-name "blarg.redhat.com"


```


注意：你需要将filename后面的值替换为真实情况下的KickstartFile文件的名字(或包含KickstartFile文件的目录)；server-name后面的值为NFS服务器名。

如果BOOTP/DHCP服务器返回的filename值以斜线(slash /)结尾，将只会被解释为路径。这样的话，客户端将挂载NFS系统的该路径，并搜索目标文件(particular file)。客户端搜索的文件名为：  + kickstart

文件名的<ip-addr>部分应该用带句点的十进制ip地址替代。例如，客户端地址为10.10.0.1对应的文件名为10.10.0.1-kickstart

注意：如果你没有指定NFS服务器(server name)，那么客户端将尝试将BOOTP/DHCP服务器作为NFS服务器进行请求。如果你没有为filename指定一个路径或文件名，客户端将尝试挂载/kickstart(mount/kickstart)BOOTP/DHCP服务器，并尝试搜索<ip-addr>-kickstart，就像上面描述的。

### HTTP Headers 

当anaconda通过网络请求kickstart时，他包含了几个用户HTTP头(custom HTTP headers)：
X-Anaconda-Architecture: x86_64  表示将安装系统的系统结构。   
X-Anaconda-System-Release: Fedora  表示将安装的系统的发行版。  
另外还有2个可选header，为kernel命令行的两个选项 [kssendsn](http://fedoraproject.org/wiki/Anaconda/Options#kssendmackssendmac]] 和 [[http://fedoraproject.org/wiki/Anaconda/Options#kssendmac)

