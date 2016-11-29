## volgroup 


用于创建一个逻辑卷管理(LVM)组。

volgroup <name> <partitions*> <options>

  *<name>
    *指定卷组名。<partitions*>(表示可以有多个分区)列出了将添加到卷组中的标示符。
  *%%--%%noformat
    *使用一个已存在的卷组。当使用此选项的时候不要指定分区。  译者注：根据之前的内physical extents容，此项应该是"使用一个已存在的卷组，且不格式化"
  *%%--%%useexisting
    *使用一个已存在的卷组。当使用此选项的时候不要指定分区。   译者注：根据之前的内容，此项应该是"使用一个已存在的卷组，且重新格式化"
  *%%--%%pesize
    *设置物理扩展大小，单位KiB
  *%%--%%reserved-space
    *specify an amount of spece to leave unused in a volume group, in megabytes.(new volume groups only)    指定卷组中的保留空间大小，单位MB。(仅对新卷组有效)
  *%%--%%reserved-percent
    *指定卷组中的保留空间占总卷组大小的百分比。(仅对新卷组有效)

首先创建一个分区，然后创建一个逻辑卷组，最后创建一个逻辑卷：


```bash


part pv.01 %%--%%size 3000   # 注：原文没有 
volgroup myvg pv.01
logvol / %%--%%vgname=myvg %%--%%size=2000 %%--%%name=rootvol


```




