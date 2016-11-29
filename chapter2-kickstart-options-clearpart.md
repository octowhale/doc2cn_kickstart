## clearpart 

删除系统分区，优先创建新分区。默认情况下不删除分区。

> [STOP_IMG](./images/stop_medium_size.png?30) 如果使用了clearpart命令，那么不能对逻辑分区使用 --nopart 选项。

  + --all
    + 删除系统上所有分区。
  + --drives
    + 指定需要删除分区的硬盘。比如，下例为清楚主IDE控制器上的前两个硬盘分区。    clearpart --all --drives=sda,sdb 
  + --list
    + 指定需要删除的分区。如果指定了，该选项将替代--all和--linux选项。该选项值来自不同硬盘。    clearpart --list=sda2,sda3,sdb1
  + --initlabel
    + 将标签初始化为符合你系统架构的默认值(例如：msdos for x86, gpt for Itanium)。该选项仅和"--all"组合使用是有效。
  + --linux
    + 删除所有linux分区
  + --none(默认值)
    + 不删除任何分区
  + --disklabel=<supported label>
    + 使用默认磁盘标签。仅当平台支持磁盘标签时有效。例如，msdos和gpt的x86_64系统支持，但dasd不支持。 在anaconda-21.43-1时引入。
