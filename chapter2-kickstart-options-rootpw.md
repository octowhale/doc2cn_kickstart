## rootpw(必要) 



该命令设置root密码为<password>。



```bash


rootpw [options] <password>


```



  + --iscrypted--plaintext
    + 如果使用--iscrypted，则密码参数被认为已加密。 --plaintext反之，密码被认为没加密。 为了创建一个加密后的密码，你可以使用python：python -c 'import crypt; print(crypt.crypt("My Password","$6$My Salt"))'。该命令通过你提供的种子(salt)产生一个sha512校验码作为你的密码。
  + --lock
    + 如果使用该项，将默认锁定root账户。这样的话，root用户将不再能够从控制台登陆。


