## keyboard 

必要

该命令为系统设置键盘类型。使用--vckeymap选项查看相关文档。本节末尾提到的技巧为“怎样使用该命令得到可接受的值”

> ![](./images/important.png?30) 从Fedora 18开始，keyboard命令有三个新选项

## arg

--vckeymap 和 --xlayouts 之一必须被使用。
另外，老格式arg任然被支持，但不能与上述两项共用。arg可以为 X layout 或者 VConsole映射表名。
缺失的值会自动从已有的值中转换。

  + --vckeymap=<keymap>
    + 指定被使用的VConsole映射表。<keymap>的值为/usr/lib/kbd/keymaps/目录中的映射表文件名，但是不包含".map.gz"后缀。
  + --xlayouts=<layout1>,...,<layoutN>
    + 指定一个被使用的X layouts列表(使用逗号分隔，而非空格)。可使用与setxkbmap(1)相同的值，但是只会使用layout格式(如：cz)或者'layout(variant)'格式(如'cz(qwerty'))之一。例如：   keyboard --xlayouts=cz,'cz (qwerty)' 
  + --switch=<option1>,...,<optionN>
    + 指定被使用的layout转换选项列表(使用逗号分隔，而非空格)。可为layout转换使用与setxkbmap(1)相同的值。	例如：    keyboard --xlayouts=cz,'cz (qwerty)' --switch=grp:alt_shift_toggle 


> 如果你只知道layout(如, Czech(qwerty))的描述，可以使用  [layouts_list.py](http://vpodzime.fedorapeople.org/layouts_list.py) 列出可用的layouts，并找出一个你需要用的。在方括号中的字符穿为有效layout规格，可被Anaconda接受。同理，可通过[switching_list.py](http://vpodzime.fedorapeople.org/switching_list.py) 
> ![idea.png](./images/idea.png?30) 查询转换选项。使用这两个脚本，必须安装libxklavier，version>=5.1-1。
