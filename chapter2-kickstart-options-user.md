user

为系统创建一个新用户



```bash


user --name=<username> [--gecos=<string>] [--groups=<list>] [--homedir=<homedir>] [--password=<password>] [--iscrypted--pliantext] [--lock] [--shell=<shell>] [--uid=<uid>] [--gid=<gid>]


```



>  ![STOP_IMG](./images/stop_medium_size.png?30) 使用Anaconda安装F19和F20时，如果不使用--password或者--lock选项，将不会为新建用户设置密码且该用户不会被锁定。这是一个bug，会在下一个版本fixed。 

  + --name
    + 指定用户名。必要选项
  + --gecos
    + 指定用户GECOS信息。该字符串包含了多个系统专有字段(system-specific fields)，以逗号分隔。经常用于指定用户的全名，办公电话等诸如此类的。通过 man 5 passwd 查看更多细节。
  + --groups
    + 额外添加默认组。各个组名之间使用逗号分隔。
  + --homedir
    + 指定用户家目录。如果没有提供，默认为 /home/<username>
  + --lock
    + 如果使用该选项，新建用户将默认被锁定。如此的话，该用户将不能通过控制台登录。
  + --password
    + 指定账户密码。如果没有指定，该账户默认将被锁定。  译者注：原文中该选项后半部分描述应该属于下一个。
  + --iscrypted--pliantext
    + 由--password提供的密码是否被加密
    + 如果使用--iscrypted，密码将被认为已加密；--pliantext则反之，被认为没加密。如果想创建一个加密的密码，可以使用python命令：python -c 'import crypt; print(crypt.crypt("My Password","$6$MySault"))'；该命令会根据你提供的种子生成一个sha512校验码。
  + --shell
    + 指定用户登录后使用的shell。如果没有提供，默认使用系统默认shell。
  + --uid
    + 指定用UID。如果没有指定，默认使用下一个可用的非系统UID。
  + --gid
    + 为用户指定主用户组。如果没指定，默认使用下一个可用的非系统GID。

