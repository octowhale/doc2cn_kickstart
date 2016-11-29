## monitor 


如果monitor命令没有被指定，anaconda会使用图形界面自动检测显示器(monitor)设置。请务必在手动配置显示器前使用该命令。

  + --hsync
    + 指定显示器的水平同步频率
  + --monitor
    + 指定显示器；该值应该从/usr/share/hwdata/MonitorsDB的hwdata包中获取显示器列表值。该显示器列表同样可以从Kickstart配置器中的图形配置界面找到。如果使用了--hsync或vsync，选项将被忽略。如果没有提供显示器信息，那么安装程序将自动进行探测。
  + --noprobe
    + 不探测显示器。
  + --vsync
    + 指定显示器的垂直同步频率


