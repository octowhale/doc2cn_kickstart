# 第三章 选择安装包 


在KickstartFile文件中使用%packages命令创建一个区块，该区块包含了被软件的列表。  
被安装的软件可以通过group或独立包名指定。安装程序定义了包含相关软件包的组(group)。参考第一CDROM中repodata/*compms.xml中关于组的列表。每个组都有一个ID，用户可见读值，名称，描述和包列表(package list)。如果一个组被选中，则其中被标记为强制的包总是会被安装；标记为默认的会被默认安装；标记为可选的包必须额外选择才会被安装。

在大多数情况下，只需要列出需要的组名而不是独立的包名。需要注意的是，核心组总是被默认选中，因此不需要在%packages区块再指定。

%packages区块必须以%end结尾。可以指定多个%package区块。如果KickstartFile作为模板并使用%include机制包含其他文件的话，会很方便。

一个关于%packages的案例：


```bash


%packages
@X Window System
@GNOME Desktop Environment
@Graphical Internet
@Sound and Video
dhcp
%end


```



正如你所见到的，指定安装包组时，每行指定一个组并以"@"开头，格式为"@+完整的组名"，完整组名通过comps.xml文件查询。组也可以通过组的id指定，如gnome-desktop。指定独立安装包时不需要其他额外的字符(如上例中的dhcp就是一个独立安装包)。

从Fedora 21开始，安装指定环境(environments)时使用"@^"前缀，并随后一个有comps.xml文件提供的完整环境名。如果多个环境被指定，只有最后一个环境将被使用。环境可以和指定组/包搭配使用(即使所指定的组不属于该环境)。

一个关于请求安装GNOME桌面环境的案例：


```bash


%packages
@^gnome-desktop-environment
%end


```



另外，指定独立安装包时可以使用通用字符。如实例：


```bash


%packages
vim*
kde-i18n-*
%end


```



该区块会安装所有以"vim"或"kde-i18n-"开头的包。

你也可以使用减号(-)取消安装某些默认列表中的包：


```bash


%packages
-autofs
-@Sound and Video
%end


```



%packages选项可以使用以下选项
  + --default
    + 安装默认包集合。在交换安装时，如果用户没有添加或删除安装包列表，将会安装默认包。
  + --excludedocs
    + 不安装包中的任何文档。在大多数情况下，意味着/usr/share/doc*中的文件不会被安装。根据包的build方式不同，也可以为其他文件。
  + --ignoremissing
    + 忽略安装在%packages区块中指定了但是在仓库中又找不到的安装包或组。默认行为是暂停(halt)安装并询问用户是否退出或继续。该选项允许全自动安装，即使出现错误也比例外。用法如下：
	%packages --ignoremissing
  + --instLangs
    + 指定语言安装列表。与选择安装包组不同。该选项并不是指定哪个安装包组需要被安装。相反，该项通过设置RPM宏命令(RPM macros)控制安装独立安装包的某个语言包(translation files)。注意：目前anaconda不支持该选项，不过可以通过pykickstart被某些软件(如 livecd-creator)识别。
  + --multilib
    + 设置yum的multilib_policy为完全(all)，而不是使用默认的最优(best)。
  + --nocore
    + 不安装@core组(默认安装)

|{{:images:stop_medium_size_.png?30|STOP_IMG}} 不安装核心组可能导致系统不能启动或者不能完成安装。谨慎使用。|

另外，%packages区块指定安装组时，可以使用以下选项：
  + --nodefualts
    + 只安装组中必须安装的强制报，而不是安装默认包
  + --optional
    + 除了安装强制包和默认包之外，还将安装可选包。该项意味着所有的安装包都会被安装。


