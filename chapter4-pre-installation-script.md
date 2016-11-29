# 第四章 预安装脚本 


你可以添加一些命令，在解析ks.cfg和处理语言、键盘和url选项完成之后，立即执行这些命令。该区块必须放在KickstartFile文件末尾(在其他命令之后)，并以%pre命令开始该区块；然后，域名服务(name service)此时还未被配置，因此只能使用IP才有效。
预安装脚本必须以%end结尾

> ![STOP_IMG](./images/stop_medium_size.png?30) 如果你的脚本产生了一个守护进程，你必须确认关闭标准输出和标准错误输出(stdout or stderr)。此乃创建守护进程的标准步骤。如果你没有关闭这些文件描述符，安装程序会挂起等待脚本运行结束。

> ![STOP_IMG](./images/stop_medium_size.png?30) 注意，预安装脚本不能在chroot环境中运行。

  + --interpreter /usr/bin/python
    + 指定解释器，脚本以不同的语言执行，如python。使用其他语言请替换/usr/bin/python位置。
  + --erroronfall
    + 如果预安装脚本出错，该选项可以产生并显示一个对话，且停止安装。该错误信息将提示错误产生位置。
  + --log
    + 指定一个文件位置，保存脚本的所有日志。


范例
一个关于%pre区块的例子


```bash


%pre
#!/bin/bash
hds=""
mymedia=""

for file in /sys/block/sd*; do
hds="$hs ${basename $file}"
done

set $hds
numhd=$(echo $#)

drive1=$(echo $hds  cut -d' ' -f1)
drive2=$(echo $hds  cut -d' ' -f2)

if [ $numhd == "2" ]  ; then
echo "#partitioning scheme generated in %pre for 2 drives" > /tmp/part-include
echo "clearpart --all" >> /tmp/part-include
echo "part /boot --fstype ext4 --size 512 --ondisk sda" >> /tmp/part-include
echo "part / --fstype ext4 --size 10000 --grow --ondisk sda" >> /tmp/part-include
echo "part swap --recommended --ondisk $drive1" >> /tmp/part-include
echo "part /home --fstype ext4 --size 10000 --grow --ondisk sdb" >> /tmp/part-include
else
echo "#partitioning scheme generated in %pre for 1 drive" > /tmp/part-include
echo "clearpart --all" >> /tmp/part-include
echo "part /boot --fstype ext4 --size 521" >> /tmp/part-include
echo "part swap --recommended" >> /tmp/part-include
echo "part / --fstype ext4 --size 2048" >> /tmp/part-include
echo "part /home --fstype ext4 --size 2048 --grow" >> /tmp/part-include
fi
%end


```


该脚本确定系统含有几个磁盘，并根据磁盘不同数量创建一个分区命令文本。在KickstartFile文件中使用引用该文本中的设置，使用如下行：


```bash



%include /tmp/part-include


```


文本中的分区命令将在安装时被使用。

