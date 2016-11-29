## sshpw 


安装器可以启动ssh以提供交互与检查，就像telnet一样。Anaconda启动ssh守护进程时，必须为内核命令行(kernel command-line)指定"inst.sshd"选项。sshpw命令用于控制安装环境中创建的账号可以远程登录。对于该命令提供的每个实例，都将创建一个用户。这些用户在安装完成后的系统上不会被创建——他们只在安装过程中存在。

需要注意的是，在默认情况下root密码为空。如果你不想任何人都可以通过ssh使用root登录设备，你必须为root指定sshpwd。同时也需要注意的是，如果anaconda解析KickstartFile文件失败，他将允许任何人以root用户登录并访问你的设备。



```bash


#
sshpw --username=<name> <password> [--iscrypted|--plaintext] [--lock]


```



  *%%--%%username
    *提供临时创建的用户名。必要选项。
  *%%--%%iscrypted|%%--%%plaintext
    *如果使用%%--%%iscrypted，则默认密码以加密。%%--%%plaintext反之，被认为密码未加密。默认值为%%--%%plaintext。
  *%%--%%lock
    *如果使用该选项，则新创建的将会被锁定。这样的话，该用户将不能通过控制台登陆。

