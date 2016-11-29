## timezone(必要) 


必要。该命令为系统设置时区。有效值为timeconfig列出的所有时区。

timezone [--utc] <timezone>

  + --utc
    + 如果使用该项，则系统将认为设备时间为UTC(格林威治)时间。

| {{:images:idea.png?30|IDEA_IMG}} 可以通过一下两种方式获取有效时区，1) 运行该脚本: http://vpodzime.fedorapeople.org/timezones_list.py ; 2) 查看该列表: http://vpodzime.fedorapeople.org/timezones_list.txt |

| {{:images:important.png?30|IMPORTANT_IMG}} 从Fedora 18开始，timezone命令有了两个新选项： |

timezone [--utc] [--nontp] [--ntpservers=<server1>,<server2>,...,<serverN>] <timezone>

  + --nontp
    + 禁止自动启动NTP服务。
  + --ntpservers=<server1>,...,<serverN>
    + 指定一个NTP服务器列表以供使用，以逗号分隔。   例如： 

```bash 


#
timezone --ntpservers=ntp.cesnet.cz,tik.nic.cz #Europe/Prague 


```



