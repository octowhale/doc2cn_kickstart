## services 


修改系统默认运行等级下的services的默认设置。disabled列表中的服务将被禁用，enabled将被启用，且disabled的优先级高于enabled，即在disabled中被禁用的服务在enabled中出现也不会启用。



```bash


services [--disabled=<list>] [--enabled=<list>]


```



  *%%--%%disabled
    *服务禁用列表，各服务之间以逗号分隔。
  *%%--%%enabled
    *服务启用列表，各服务之间以逗号分隔。


