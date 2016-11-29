## firstboot 
设置设置代理程序(Setup Agent)是否在系统初次启动时运行。如果为enabled，则必须安装initial-stup包必须被安装。如果没指定，设置代理(initial-setup)默认为disabled。

 firstboot %%--%%enable|%%--%%disable|%%--%%reconfig 
  *%%--%%enable 或者 %%--%%enabled
    *系统第一次启动时，运行设置代理程序。
  *%%--%%disable or %%--%%disabled
    *系统初次启动时，不运行设置代理程序。
  *%%--%%reconfig
    *在重新配置模式(reconfiguration mode)中，初起系统时，运行设置代理程序。该模式中，将设置下列选项为默认值，包括语言、鼠标、键盘、root密码、启动等级、时区和网络配置选项。

