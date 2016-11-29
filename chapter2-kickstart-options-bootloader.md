## bootloader(必选) 

必选命令。指出boot loader是怎么被安装的。
> [important.png](./images/important.png?30) **BIOS引导分区**    对Fedora 16而言，必须为系统分配biosboot分区并安装GPT/GUID分区表，这样便可通过anaconda进行磁盘初始化。可以通过kickstart命令 part biosboot --fstype=biosboot --size=1  进行分区。然而，为了防止磁盘已存在一个biosboot分区，使用"part biosboot"命令并不是必须的。

  + `--append`
    + 指定内核参数。bootloader的默认设置为 "rhgb quiet"。 无论给 `--append` 传递任何参数，或者完全--append，你都将获得这个"rhgb quiet"这个参数。例如：  `bootloader --location=mbr --append="hdd=ide-scsi -ide=nodma"`
  + `--boot-drive`
    + 指定引导程序写入的分区，系统启动时，从该分区引导。
  + `--disabled`
    + 不安装引导程序
  + `--leavebootorder`
    + 在EFI或者ISeries/PSeries机器上，该选项可以保护已存在的启动镜像(bootable image)不被安装器所修改。
  + `--dirveorder`
    + 指定磁盘分区在BIOS中的启动顺序，例如： `bootloader --driverorder=sda,hda`
  + `--location`
    + 指定引导记录的安装位置。有效值为：mbr(默认)、partition(在分区第一扇区安装包含内核的引导程序)、none(不安装引导程序)
  + `--password`
    + 如果使用了GRUB，则为GRUB引导程序设置密码。该项用于限制访问GRUB shell(GRUB shell可以随意传递参数)
  + `--iscrypted`
    + 如果指定了该项，加密由--password=的密码，并不在做额外的修改，传递给引导程序设置。
  + `--md5pass`
    + 如果使用了GRUB，除了改密码已经被加密之外，其他与选项 `--password=` 相似。
  + `--timeout=<secs>`
    + 指定引导程序的超时时间(秒)，超时后使用默认启动选项。
  + `--default`
    + 在引导程序配置默认启动镜像。
  + `--extlinux`
    + 使用extlinux引导程序取代GRUB。 该选项尽在支持extlinux的设备上有效。