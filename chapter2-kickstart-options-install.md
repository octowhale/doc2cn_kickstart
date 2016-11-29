## install (默认) 



为设备安装一个全新的系统，而非对已有的系统进行升级。默认模式。
必须为安装程序指定来源，cdrom、硬盘、nfs或者url(如果支持ftp/http安装)。安装命令与安装方法命令必须以竖线分割。

>  [](./images/important.png?30)  Fedora18及以后版本系统需要注意，anaconda不再对其支持升级操作。替代工具为，Fedora升级工具的FedUp。  

### cdrom 


  + cdrom
    + 从第一光驱启动安装系统。

### harddrive 

]  

> 从本地硬盘上的ISO镜像目录安装系统，硬盘文件系统必须为vfat或者ext2。在目录中，你需要必须提供install.img，以使用boot.iso启动或者在ISO镜像的同级目录创建一个images目录并放入install.img。
  + --biospart
    + 指定BIOS分区安装源(如，82p2)
  + --partition
    + 分区安装源 (如，sdb2)
  + --dir
>     + 该目录包含ISO镜像和images/install.img。例如：     harddrive --partition=hdb2  *--dir=/tmp/install-tree 

### liveimg 



] [--noverifyssl] 

安装一个磁盘镜像而不是软件包。该镜像可以为现在ISO中的squashfs.img，或者能被安装媒体挂在的文件系统(如，ext4)。Anaconda希望该镜像能包含完全安装系统所需要的所有工具，因此，最好的方法是使用livemedia-creator创建一个磁盘镜像。如果镜像宝箱了/LiveOS/*.img(squashfs.img的目录结构)，那么LiveOS目录中的第一个img文件将被挂在并用于安装目标系统。在Anaconda 21.29中，URL可能指向根文件系统中的一个压缩文件(tarfile),该文件必须以 .tar,.tbz,.tgz,.txz,.tar.bz2,.tar.gz,.tar.xz结尾。

  + --url
    + 通过URL指定安装源。支持http,https,ftp和file协议
  + --proxy=[protocal://][username[:password]@]host][:port]
    + 指定执行安装时所使用的HTTP/HTTPS/FTP代理。根据实际情况填写上述地址的各个部分。
  + --checksum
    + 可选项，使用sha256校验该镜像文件。
  + --noverifyssl
    + 如果使用HTTPS服务器提供的目录树，不检查服务器证书或证书与服务器主机名是否一致。

### nfs 


]  

从指定的NFS服务器上安装。可以为展开的安装程序目录树或者包含ISO镜像的目录。对后者而言，和harddrive安装方法一样，需要提供一些必要的文件，详细参考harddrive的描述。

  + --server
    + 指定安装源所在的服务器(主机名或ip地址)
  + --dir
>     + 包含软件包/目录的安装程序目录树的目录。如果是通过ISO安装，该目录必须包含images/install.img。
  + --opts
    + 挂载NFS是所需要用到的挂载参数。可以使用任何通过/etc/fstab中挂载NFS时允许使用的参数。可以通过man 5 nfs查看选项列表。多个选项之间使用逗号隔开。如：   nfs --server=nfsserver.example.com --dir=/tmp/install-tree  
	

### url 

] [--noverifyssl]   

通过FTP/HTTP进行安装

  + --url
    + 指定安装源的URL。在URL中，可以使用$releaseve和$basearch进行替换。(Fedora19中引入)
  + --mirrorlist
    + 安装源的mirror URL。在URL中可以使用$releaseve和$basearch进行替换。(Fedora19中引入)
  + --proxy=[protocal://][username[:password]@]host[:port]
    + 指定HTTP/HTTPS/FTP代理。根据实际情况填写上述地址的各个部分。
  + --noverifyssl
    + 如果使用HTTPS服务器提供的目录树，不检查服务器证书或证书与服务器主机名是否一致。
