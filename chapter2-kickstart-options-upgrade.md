## upgrade 


>  ![IMPORTANT_IMG](./images/important.png?30)  Fedora 18及更新系统需要注意，anaconda将不再支持使用upgrades。取而代之的是使用FedUp，一款Fedora更新工具。 

告诉系统进行升级，而不是重装一个新系统。你必须指定安装树的位置，如cdrom,harddrive,nfs或者url(/ftp/http)。参考install的详细信息。

  + --root-device=<root>(可选)
    + 在单机多系统环境(On a system with multiple installs)，该选项指定某一个文件系统需要进行升级(upgraded)。可以通过设备名，UUID=<uuid>或LABEL=指定，和harddrive命令差不多。

