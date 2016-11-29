## device 

在大部分PCI系统上，安装程序会自动探测Ethernet和SCSI卡。在老系统或部分PCI系统上，kickstart需要指定查找合适的设备。device命令会告诉安装程序安装额外模块。   
 
  + <moduleName>
    + 需要被安装的，用于替代内核模块的模块名称。
  + --opts
    + 指定传递给内核模块的参数列表。例如：   `+ -opts="aic152x=0x340 io=11" `

