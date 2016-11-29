## ignoredisk 


控制anaconda访问系统硬盘。选项--drivers和--only-use之间互斥。
  *  ignoredisk --drivers=[disk1,disk2,...]  
    *指定某些硬盘在进行分区、格式化和清理(partitioning,formatting,clearing)时不能被anaconda访问。
  * ignoredisk --only-use=[disk1,disk2,...]  
    *与--drivers相反。这里只列出需要在安装过程中被处理的硬盘。
  * ignoredisk --interactive 
    *允许用户手动设置。

