## %ksappend 


The %ksappend url directive is very similar to %include in that it is used to include the contents of additional files as though they were at the location of the %ksappend directive. The difference is in when the two directive are processed. %ksappend is processed in an initial pass, before any other part of the kickstart file. Then, this expanded kickstart file is passed to the rest of anaconda where all %pre scritps are handled, and then finally the rest of the kickstart file is processed in order, thich includes %include directive.
Thus, %ksappend provides a way to include a file containing %pre scripts, while %include does not.

%ksappend ur指令与%include指令相似，都可以从另一个中引用其内容到当前位置。不同的是二者被处理的时间。%ksappend最先被处理，在KickstartFile文件中的其他任何部分之前。然后该扩展后的KickstartFile文件被传递给负责所有%pre脚本的anaconda，最后剩下的KickstartFile文件按顺序被处理，其中包括%include指令。
因此，%kisappend提供了一种方式引用文件，且该文件包含%pre脚本。而%include不能。