## logvol 


为逻辑卷管理(LVM)创建逻辑卷

logvol <mntpoint> %%--%%vgname=<name> %%--%%size=<size> %%--%%name=<name> <options>

  *%%--%%noformat
    *使用一个已有的逻辑卷且不进行格式化。
  *%%--%%useexisting
    *使用一个已有的逻辑卷，并重新格式化。
  *%%--%%fstype
    *为逻辑卷指定文件系统类型。有效值包括ext4,ext3,ext2,btrfs,swap和vfat。其实文件系统是否有效取决于命令行传递给anaconda的参数是否启动这些文件系统。Btrfs目前正在测试中。使用该命令前记得备份。
  *%%--%%grow
    *通知逻辑卷填充可用空间(如果有)，或者提高容量最大值设置。需注意，%%--%%grow不能用于RAID卷上。
  *%%--%%maxsize
    *设置逻辑卷扩展最大容量(单位MB)。值为整数，不要接单位MB。如 %%--%%maxsize=10
  *%%--%%recommended
    *让系统自动设置逻辑卷大小
  *%%--%%percent
    *为逻辑卷指定大小时，使用卷组中可用空间的百分比。如果使用了%%--%%grow选项，该选项无效。
  *%%--%%encrypted
    *加密逻辑卷
  *%%--%%passphrase
    *加密逻辑卷时使用的密码。如没使用%%--%%encryped，该项无效。如果没有指定密码，则会默认使用系统密码；如果没有系统密码，安装器会停止并提示。
  *%%--%%escrowcert=<url>
    *通过<url>加载一个X.509证书。保存该逻辑卷的秘钥，加密使用该证书，作为文件放在/root下。当使用了%%--%%encryped时有效。
  *%%--%%backuppassphrase
    *当使用了%%--%%escrowcert时有效。除了保存秘钥数据之外，还会为该逻辑卷生成一个随机密码。之后保存该密码，通过%%--%%escrowcert指定的证书加密，作为文件放在/root下。如果不止一个LUKS卷使用了——-backuppassphrase，那么所有的卷都会使用相同的密码。
  *%%--%%thinpool
    *创建一个thin pool逻辑卷。(使用none作为挂载点)
  *%%--%%metadatasize=<size>
    *为新创建的thin pool设备指定metadata area大小(单位MiB)
  *%%--%%chunksize=<size>
    *为新创建的thin pool设备指定chunk大小(单位KiB)
  *%%--%%thin
    *创建一个thin逻辑卷。(需要搭配使用%%--%%poolname)
  *%%--%%poolname=<name>
    *为thin pool指定一个名字以创建thin逻辑卷。(需要搭配使用%%--%%thin)
  *%%--%%resize
    *尝试使用%%--%%resize=指定的值重置逻辑卷大小。该选项必须与%%--%%useexisting %%--%%size=搭配使用，否则会报错。

首先创建一个分区，其次创建一个逻辑卷组，最后创建一个逻辑卷。例如：   

```bash


part pv.01 --size 3000
volgroup myvg pv.01
logvol / --vgname=myvg --size=2000 --name=rootvol


```



