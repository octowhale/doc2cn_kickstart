## repo 


配置额外的YUM仓库，该仓库可能被用作软件源。可以指定多行仓库。默认的，在使用媒体时，anaconda在/etc/anaconda.repos.d设置了一些仓库，并额外添加一个特殊安装仓库。这些仓库的精确设定根据发行版不同而不同，无法在这里列出。可能会有一个叫做"updates"的仓库。

注意：如果你要在/etc/anaconda.repos.d中启用默认禁用的仓库(如，"updates")，你需要使用%%--%%name=<repoid>，而不是其他选项。anaconda会自动查找该名字的仓库。提供一个baseurl或者mirrorlist URL会导致anaconda尝试额外添加一个相同名字的仓库，这样会导致仓库冲突错误。


```bash


repo --name=<name> [--baseurl=<url>|--mirrorlist=<url>] [options]


```




  *%%--%%name
    *仓库id。必要选项。如果新仓库名与之前添加的发生冲突，则新仓库将被无视。因为anaconda在开始的时候提供了一个仓库列表，这意味着用户不能使用这些名字创建新仓库。通过查看你想安装的操作系统的/etc/anaconda.repo.d目录获取哪些仓库名已被占用。
  *%%--%%baseurl
    *仓库的URL。那些在yum仓库配置文件中的参数，可能在这里不被支持。该选项与%%--%%baseurl之间只能选择一个。如果指定了一个NFS仓库，URL格式应该为 %%nfs://host:/path/to/repo%%。注意，在host后面有一个冒号%%--%%Anaconda会将%%"nfs://"%%后面的所有东西直接传递给mount命令，而不是分析URLs语法(参考[RFC 2224](http://tools.ietf.org/html/rfc2224))。可以在url中使用$releasever和$basearch变量替换，从Fedora19后加入。
	译者注：根据RFC 2224，客户端连接nfs是省略:port，将使用默认端口2049。那么NFS使用非标准端口，应该怎么写？
  *%%--%%mirrorlist
    *指向仓库镜像列表的URL。在仓库配置文件中使用的部分变量可能不被支持。该选项与%%--%%baseurl之间只能选择一个。可以在url中使用$releasever和$basearch变量替换，从Fedora19后加入。
  *%%--%%cost
    *为该仓库指定一个整数作为优先级。如果多个仓库提供相同的安装包，该数字将作为优先级判断。数字越小，优先级越高。
  *%%--%%excludepkgs
    *指定不从该仓库获取的安装包名和组名，多个之间用逗号分隔。该项用于多个仓库提供相同的安装包时，你想知道该包是从哪个仓库获取的。
  *%%--%%includepkgs
    *指定必须从该仓库获取的安装包名和组名，多个之间用逗号分隔。该项用于多个仓库之间提供相同的安装包时，你想知道该包是从哪个仓库获取的。
  *%%--%%proxy=%%[protocol://][username[:password]@]host[:port]%%
    *为该仓库指定一个HTTP/HTTPS/FTP代理。该设置不影响其他仓库，也不影响使用HTTP安装时获取install.img。url中多个参数根据实际情况填写。
  *%%--%%ignoregroups=true
    *该选项用于组成安装树(composing installation trees)，但对安装程序本身没有影响。他告诉compose tools在反射(mirroring)树是不考虑包组(package group)信息，以避免反射太多不需要的数据。
  *%%--%%noverifyssl
    *对于https仓库，不检查服务器证书是否有效，且不检查服务器名与证书域名是否匹配。
  *%%--%%install
    *安装该仓库到目标系统，并在重启后应用。anaconda-22.3-1中引入。



