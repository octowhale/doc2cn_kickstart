## driverdisk 

驱动磁盘可用于kickstart安装过程中。你需要拷贝驱动盘中的内容到系统硬盘上的一个分区的根目录下。然后使用dirverdisk告诉安装程序到哪儿寻找驱动盘。 



  *<partition>
    *包含驱动盘的分区
  *%%--%%sourc=<url>
    *为启动盘指定一个URL。NFS可以使用该命令该位置： nfs:host:/path/to/img  
  *%%--%%biospart=<part>
    *包含驱动盘的BIOS分区(例如：82p2)

