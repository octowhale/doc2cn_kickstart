## part or partition(必要) 

为系统创建分区。必要选项

| {{:images:stop_medium_size_.png?30|STOP_IMG}} 在不使用--noformat和--onpart的情况下，所有被创建的分区都会被格式化。 |

  + part <mntpoint>    <mntpoint>为分区挂载点，必须遵守以下格式：
    + /<path>
    +   例如，/,/usr,/home
  + swap
    +   分区用作交换空间    使用--recommended选项，可以自动设置交换分区大小。从Fedora 18开始，为了支持系统休眠，可以使用--hibernation选项可以用于自动设置足够大的交换分区空间。
  + raid.<id>
      +   该分区将用作软RAID(参考RAID)
  + pv.<id>
    +   该分区将用作LVM(参考logvol)
  + btrfs.<id>
    +   该分区将用作BTRFS卷(参考btrfs)
  + biosboot
    +  该分区将用作BIOS启动分区。Fedora 16中，必须为bootloader创建一个biosboot分区且拥有GPT/GUID分区表(参考bootloader)。
  + --size
    + 设置分区大小最小值(单位MB)。等号后只接整数，如500。不要再接MB。
  + --grow
    + 设置分区占用所有可用空间(如果有)，或者设置磁盘空间扩展后的最大(上限)值。注意，RAID卷上的分区不支持--grow选项。
  + --maxsize
    + 设置分区大小的最大值，如果设置了磁盘增长(--grow不能超过此值)。
  + --noformat
    + 使安装程序不对分区进行格式化，与--onpart命令一起使用
  + --onpart= or --usepart= 
    + 在已存在的设备上建立分区。通过使用标签(label)或UUID指定分区。命令为"--onpart=LABEL=name"或者"--onpart=UUID=name"   

| {{:images:stop_medium_size_.png?30|STOP_IMG}}  Anaconda以特有的顺序创建分区，相较而言，使用标签比只使用分区名更为安全。 |

  + --ondisk= or --ondrive
    + 强制指定在某一磁盘上建立分区。
  + --asprimary
    + 强制自动分配该分区为主分区。否则分区失败。    | {{:images:idea.png?30| IDEA_IMG}} --asprimary选项仅在MBR分区中有效。当使用GPT分区时将被忽略。|
  + --fsprofile
    + 在该磁盘上创建文件系统的程序指定一个使用类型(usage type)。该使用类型定义了一系列创建文件系统时将使用的参数。为了该选项能正常工作，该文件系统必须支持使用类型且必须有一个包含所有可用类型的配置文件。对ext2/3/4而言，该配置文件为 /etc/mke2fs.conf
  + --fstype
    + 设置分区文件系统类型。有效值为 ext4/3/2,swap,btrfs,vfat。其他文件系统是否有效取决于传递给anaconda命令行的参数是否启用这些文件系统。
  + --fsoptions
    + 为挂载该文件系统指定一串自由格式的挂载参数字符串。该字符串将被复制到完成安装系统的/etc/fstab文件内，并使用括号括起来。
  + --label
    + 为该分区上要创建的文件系统指定标签。
  + --recommended
    + 自动分配分区大小。
  + --onbiosdisk
    + 在特定磁盘上穿件一个由BIOS发现的分区。
  + --encryped
    + 加密该分区。
  + --passphrase
    + 为该分区指定加密时使用的密码。如果没有指定--encryped，该选项将无效。如果没有指定密码，则会使用默认系统密码，如果没有系统密码安装将会停止并提示。
  + --encrowcert=<url>
    + 从<url>加载X.509证书。在/root下的某文件内保存该分区数据秘钥，使用该证书加密。只有在指定了--encryped时有效。
  + --backuppassphrase
    + 只有在制定了--encrowcert时有效。在该分区中额外储存数据秘钥，生成一个随机密码。然后保存该密码，并使用--escrowcert指定的证书加密。如果超过一个LUKS卷使用--backuppassphrase,那么在这些卷上将使用相同的密码。
  + --resize
    + 接收--size=的值，并重置该分区大小。该选项必须与--onpart --size=一起使用，否则会报错。  
 
| {{:images:stop_medium_size_.png?30|STOP_IMG}}  如果分区过程中出现任何错误，将会在虚拟控制台3上打印诊断信息。 |


