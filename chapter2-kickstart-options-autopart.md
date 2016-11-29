## autopart 

自动创建分区

一个root分区，一个swap分区，一个符合架构体系的boot分区。在足够大的硬盘上，还会创建一个 /home 分区

> ![stop_medium_size.png](../images/stop_medium_size.png?30) autopart命令不能与part/partion,raid,volgroup或logvol命令在同一个KickstartFile中互斥。

  + `--type=<type>`
    + 选择自动分区机制(schema)。type值必须为下列之一：lvm,btrfs,plain,thinp. Plain是指非btrfs或lvm的常规分区。
  + `--nolvm`
    + 同 `--type=plain`
  + `--encrypted`
    + 默认加密所有支持加密的设备。 该选项与初始化分区界面中的 "Encrypt" 选项一致。
  + `--passphrase`
    + 仅在设置了 `--encrypted` 时有效。 为加密设备提供一个全局系统的默认密码。
  + `--escrowcert=<url>`
    + 仅在设置了 `--encrypted` 时有效。 从 `<url>` 加载一个X.509证书。在/root目录下以文件的形式存储所有安装过程中创建的加密卷的密钥。 
  + `--backuppassphrase`
    + 仅在设置了 `--encrypted` 时有效。 除了存储数据密钥之外，在所有安装过程中产生的加密卷中加入随机生成的密码。然后在/root目录下以文件的形式存储这些使用 `--escrowcert` 指定的认证加密过的密码。(每个加密卷对应一个文件) 
  + `--cipher`
    + 仅在设置了--encrypted时有效。特别是在加密算法需要被用于加密文件系统时。
  + `--fstype=<filesystem>`
    + 为分区指定文件系统格式。注意，在分区机制与文件系统都为btrfs时，不能使用 `--type=btrfs` 。 例如：`--fstype=ext4` 。 在anaconda-21.46-1引入
