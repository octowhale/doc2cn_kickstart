## raid 


配置一个软RAID设备。命令格式为：
raid <mntpoint> --level=<level> --device=<mddevice> <partitions*>

  + <mntpoint>
    + 指定RAID文件系统挂载点。如果为根目录(/)，RAID等级(level)必须为1，除非启动分区(/boot)已存在。如果启动分区存在，/boot分区等级必须为1，而根分区(/)等级可以为任意可用的类型。<partitions*>(表示可以使用多个分区)列举了加入RAID组中的RAID标示符。
  + --level
    + RAID等级类型，有效值为0,1,4,5,6,10。
  + --device
    + 为RAID设备命名(如，"fedora-root"或"home")。从Fedora 19开始，RAID设备不能再通过'md0'类似的名字被引用。如果你有一个老(v0.90 metada)，你不能为该阵列分配名字，但是你可以通过文件系统标签或者UUID指定阵列(如，--device=LABEL=fedora-root)。
  + --spares
    + 为RAID阵列分配备用磁盘数量。在RAID阵列出现错误的时候，可以用备份磁盘恢复。
  + --fstype
    + 指定RAID阵列文件类型。有效值包括ext4,ext3,ext2,btrfs,swap和vfat。其他文件系统是否支持取决于传递给anaconda命令行的参数是否启用这些文件系统。
  + --fsoptions
    + 为挂载文件系统时指定一个无格式的字符串作为挂载选项(option)。该字符串应该被双引号括起来，并将被复制到完成安装的系统的/etc/fstab文件中。
  + --label
    + 为安装的文件系统指定标签。如果该标签已被使用，则会创建一个标签。
  + --noformat
    + 使用已存在的RAID设备，并且对该阵列进行格式化。
  + --useexisting
    + 使用已存在的RAID设备，并格式化。
  + --encrypted
    + 加密该RAID设备。
  + --passphrase
    + 为加密RAID设备指定一个密码。如无--encrypted选项，则该项无效。如果没有指定密码，则会使用默认系统密码；如果没有系统密码，安装器将会停止并提示。
  + --encrowcert=<url>
    + 从<url>加载一个X.509证书。使用该证书加密，并保存该RAID设备的数据秘钥至/root下的一个文件。仅当使用了--encrypted是有效。
  + --backuppassphrase
    + 仅当使用了--escrowcert是有效。在该阵列设备中额外保存数据秘钥，并生成一个随机密码。使用--escrowcert指定的证书进行加密，并保存改密码到/root下的一个文件中。如果不止一个LUKS卷使用了--backuppassphrase，则这些卷都将使用一个相同的密码。

该示例展示了怎样为根目录(/)创建一个RAID 1 阵列，为/usr创建一个RAID 5 阵列，该系统有三个磁盘。同时为每个磁盘创建一个交换(swap)分区，共三个。


```bash



part raid.01 --size=6000 --ondisk=sda
part raid.02 --size=6000 --ondisk=sdb  
part raid.03 --size=6000 --ondisk=sdc

part swap1 --size=512 --ondisk=sda
part swap2 --size=512 --ondisk=sdb
part swap3 --size=512 --ondisk=sdc

part raid.11 --size=6000 --ondisk=sda
part raid.12 --size=6000 --ondisk=sdb
part raid.13 --size=6000 --ondisk=sdc

raid / --level=1 --device=md0 raid.01 raid.02 raid.03
raid /usr --level=5 --device=md1 raid.11 raid.12 raid.13


```




