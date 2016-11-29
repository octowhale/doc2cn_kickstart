# 第一章 kickstart简介 
## 什么是Kickstart安装工具 
许多系统管理员在安装Fedora或Red Hat Enterprise Linux(RHEL)系统时，更愿意使用一种自动化安装的方法。为了满足这种需求，Red Hat开发了kickstart安装工具。通过kickstart，系统管理员可以创建一个文件--包含使用手动安装时会遇到的所有交互问题的答案。

Kickstart文件(KickstartFile)可以被保存在服务端系统(server system)上，客户端安装系统时可以读取该文件。该安装工具支持在多种设备上使用一个单独的kickstartFile进行安装Fedora或RHEL，是网络和系统管理员的理想之选。

Fedora安装向导 http://docs.fedoraproject.org/en-US/index.html 有关于kickstart的详细章节。

## 怎样使用Kickstart进行安装 
Kickstart安装工具可以被运行在本地CDROM，本地硬盘，或者NFS、FTP、HTTP上。
运行kickstart，必须满足以下几点：
  -创建一个kickstartFile。
  -创建一个带有kickstartFile的启动磁盘，或确保kickstartFile能在网络中可用。
  -确保安装树可用
  -启动kickstart安装工具
本章将详细解释这些步骤。

## 创建KickstartFile 
KickstartFile只是一个单纯的文本文件(text file)，包含了一个所有项目(Items)的列表，每个项目都由一个关键字(keyword)识别。可以通过Kickstart Configurator程序或其他文本编辑器创建KickstartFile。Fedora或RHEL安装工具也可以通过一些参数选项生成一个简单KickstartFile，该文件被保存为 /root/anaconda-ks.cfg 。你可以通过文本编辑器将其另存为一个ASCII文件。

首先，在你创建KickstartFile时，需要注意以下几点：
  *虽然不是必须的，随后章节中提到了一些约定俗成的用法。如果有特别说明，项目(Items)的用法可以不遵守随后章节中的内容。
    -命令 -- 参考第2章中的kickstart选项列表。必须包含一些必要选项。
    -%packages -- 参考第3章的详细信息
    -%pre、%post和%traceback -- 这些部分可以以任意顺序进行拍了，且不是必须的。参考第4章和第5章的详细信息。
  *%packages、%pre、%post和%traceback部分都必须以%end结尾。
  *不必要的项目可以被忽略
  *忽略任何必须项目将会导致安装过程中需要用户手动处理这些项目，就像之前的手动安装一样。一旦这些项目被处理，将会继续进入无人值守状态，直到找不到下一个必要项目的应答内容。
  *#开始的行用作注释，执行时将被忽略
  *安装过程中遇到了不推荐的命令、选项或参数，警告消息将会保存到anacoda日志中。一些发行版通常会删除这些不推荐项目。通过检查安装日志确认没有使用这些不推荐命令、选项或参数。当使用ksvalidator时，不推荐项目会引发一个错误。

## 引用硬盘时的特殊说明 
习惯上，整个kickstart安装过程中，硬盘以设备节点名(如sda)被引用。然而Linux内核使用了一种更为动态的方法，而无法保证系统重启后硬盘节点名不发生变化，这样就是kickstart脚本复杂化了。为了保证设备名的稳定性，你可以使用类似/dev/disk来取代设备节点名。例如，为了取代


```bash


part / --fstype=ext4 --onpart=sda1


```



你可以使用随后类似的命令：


```bash


part / --fstype=ext4 --onpart=/dev/diskk/by-path/pci-0000:00:05.0-scsi-0:0:0:0-part1
part / --fstype=ext4 --onpart=/dev/disk/by-id/ata-ST3160815AS_6RA0C882-part2


```



这样便为引用硬盘提供了一个持续不变的方法，且比仅仅使用sda显得更明确。这种方法在大存储环境中特别有用。

你也可以使用shell-like入口引用硬盘。这种方法主要用于大存储环境中方便使用clearpart和ignoredisk命令。
例如，为了取代：


```bash


ignoredisk --drives=sdaa,sdab,sdac


```



你可以使用以下类似命令：


```bash


ignoredisk --drives=/dev/disk/by-path/pci-0000:00:05.0-scsi-*


```



最后，在任何地方你想引用一个已存在的分区或文件系统(使用，"part --ondisk=")选项,你可以使用文件系统的标签(label)或UUID。例如：


```bash


part /data --ondisk=LABEL=data
part /misc --ondisk=UUID=819ff6de-0bd6-4bf4-8b72-dbe41033a85b


```



