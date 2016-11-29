## btrfs 
(在anaconda-17.3引入)

定义BTRFS卷或子卷。

定义卷：


```bash



btrfs <mntpoint> --data=<level> --metadata=<level> --label=<label> <partitions*> 


```



定义子卷：


```bash```


<partitions*>(可以为多个分区)为添加到BTRFS卷中的BTRFS标示符。对子卷而言，<parent>应指定子卷的父卷的标示符。

  + <mountpoint>
    + 指定文件系统挂载点
  + --data
    + 文件系统数据(data)的RAID等级(0,1,10)。可选项。该选项对子卷无效。
  + --metadata
    + 文件系统/卷元数据(metadata)的RAID等级(0,1,10)。可选项。该选项对子卷无效。
  + --label
    + 为文件系统指定标签。如果该标签已被使用，则会创建一个新标签。该选项对子卷无效。
  + --noformat
    + 使用现有的BTRFS卷(或子卷)，且不进行格式化。
  + --useexisting
    + 与--noformat相同

该例子展示了怎样在三个硬盘上通过成员分区创建BTRFS卷，并为root和home创建子卷。本示例中并没有展示主卷被挂载或使用，仅展示root和home子卷。



```bash


part btrfs.01 --size=6000 --ondisk=sda
part btrfs.02 --size=6000 --ondisk=sdb
part btrfs.03 --size=6000 --ondisk=sdc

btrfs none --data=0 --metadata=1 --label=f17 btrfs.01 btrfs.02 btrfs.03
btrfs / --subvol --name=root LABEL=f17
btrfs /home --subvol --name=home LABEL=f17
# 注：原文/home中没有LABEL，应该为笔误
#btrfs /home --subvol --name=home f17


```

