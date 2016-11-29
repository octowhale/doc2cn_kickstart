realm
Join an Active Directory or FreeIPA domain
加入一个活动目录或FreeIPA域



```bash


realm join <domain.example.com>


```



  + --computer-ou
    + 为计算机指定一个唯一的名字(distinguished nme)以在域(organizational unit)中创建计算机账户。该名字的精确格式依赖于客户端软件和成员资格软件。你通常可以省略该名称的域名部分(root DES portion)。注：这里的翻译是根据自己理解，并未完全按照原文字翻译。
	
  + --no-password
      + 加入域是不适用密码
  + --one-time-password
      + 加入域是使用一个一次性密码。该项不一定适用于所有域或活动目录。
  + --client-software
      + 只加入可以使用指定客户端软件的域。可能有效值包括sssd或winbind。不是所有值都支持所有域。默认客户端软件由系统自动选择。
  + --server-software
      + 只加入运行指定服务端软件的域。可能有效值包括avtive-directory或freeipa。
  + --membership-software
      + 加入域时所使用的软件。可能有效值为samba或adcli。并非所有值都适用于所有域。默认成员关系软件为系统自动选择。



```bash


realm join --one-time-password=12345 DC.EXAMPLE.COM


```


