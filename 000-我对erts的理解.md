#<center>我对Erts的理解</center>

很多人将Erts比喻成操作系统，这个比喻确实很贴切。	
Erts的大牛们很细致的将Erts分成了下面的几个部分。


	核心：提供BIF操作，各种平台级别的封装，ring0进程等
	驱动：提供TCP/IP驱动，文件驱动，zip驱动
	init进程：初始化进程

