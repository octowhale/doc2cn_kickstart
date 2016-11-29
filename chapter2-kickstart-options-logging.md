logging

该命令用于控制安装过程中anaconda产生的错误日志，对已安装成功的系统没有影响。

  *%%--%%host
    *设置接受logging信息的远程主机，该主机必须启动syslogd进程，并设置为可接受远程logging。
  *%%--%%port
    *指定远程syslogd进程所使用的端口，如果远程syslogd进程未使用默认端口。
  *%%--%%level
    *指定日志等级。值为debug,info,warning,error或critical之一。   	为tty3上显示的日志信息指定最小等级。不管怎样该等级如何设置，所有日志都会被发送到日志文件中。

