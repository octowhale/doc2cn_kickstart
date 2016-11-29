## vnc 


允许通过VNC远程图形模式安装过程。该方法通常不建议文本模式使用，因为文本模式安装时有一些大小和语言显示。在不使用其他选项时，该命令会在本机运行一个不需要密码访问的VNC服务器，并且打印出远程设备连接时需要的命令。

vnc [--host=<hostname>] [--port=<port>] [--password=<password>]

  + --host
    + 连接--host指定的主机监听的VNC viewer进程，而不是在安装设备上启动一个VNC服务端。
  + --port
    + 提供一个远程VNC viewer进程监听的端口，如果没有提供，anaconda将使用VNC默认端口。
  + --password
    + 设置VNC连接时使用的密码。可选项，但是推荐指定。

