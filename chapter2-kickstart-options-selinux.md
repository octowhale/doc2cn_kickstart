## selinux 


设置安装完成后系统的SELinux状态，anaconda中，SELinux默认值为enforcing



```bash


selinux [--disabled|--enforcing|--permissive]


```



  *%%--%%disabled
    *禁用selinux
  *%%--%%enforcing
    *设置selinux为强制模式
  *%%--%%permissive
    *宽恕模式。启用selinux，但是只记录将被强制模式拒绝的事情。

