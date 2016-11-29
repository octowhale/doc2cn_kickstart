# 第五章 追加安装脚本 


使用该选项添加一些命令，只有在安装结束时才被执行。该区块必须在KickstartFile文件结尾，且以%post命令开头。该区块还是比较有用，比如说安装一些软件，或配置一个备用DNS服务器。

可以同时使用多个%post区块，这对部分区块在chroot环境执行而部分区块不在chroot环境执行的情况很有用。

每个%post必须以%end结尾。

|{{:images:stop_medium_size_.png?30|STOP_IMG}} 如果你使用静态IP配置网络，包括一个nameserver，你可以在%post区块中访问网络并解析主机名(resolve ip address)。如果你使用DHCP配置网络，在执行%post区块时/etc/resolv.conf还不完全，你可以访问网络，但是不能解析主机名。因此，如果你使用DHCP，你必须之在%post区块中指定IP地址。|

|{{:images:stop_medium_size_.png?30|STOP_IMG}} 如果你的脚本会产生一个守护进程，那么你必须关闭stdout和stderr。这是创建守护进程的标准步骤。如果你不关闭这个文件描述符，安装过程会被挂起直到scripts执行完毕。|

|{{:images:stop_medium_size_.png?30|STOP_IMG}} post-install脚本在chroot环境中执行，因此类似复制脚本或安装RPMs之类的任务执行时将会失效。|

  + --nochroot
    + 指定该选项后，允许命令在chroot环境外执行。
  + --interpreter /usr/bin/python
    + 指定执行脚本的语言，如python。使用其他语言替换/usr/bin/python
  + --erroronfall
    + 如果追加脚本执行出错，该选项会产生一个对话并打印，且停止安装。该错误信息将提示产生错误的位置。
  + --log
    + 将日志信息保存至指定的文件中。

范例
执行一个在NFS共享中名为runme的脚本


```bash


%post
mkdir /mnt/temp
mount 10.10.0.2:/usr/new-machines /mnt/temp
open -s -w -- /mnt/temp/runme
umount /mnt/temp
%end


```



将/etc/resolv.conf文件复制到新安装的系统中


```bash


%post
cp /etc/resolv.conf /mnt/sysimage/etc/resolv.conf
%end


```



|{{:images:stop_medium_size_.png?30|STOP_IMG}} 如果通过livecd-creator工具运行kickstart，你应该将/mnt/sysimage换成$INSTALL_ROOT

