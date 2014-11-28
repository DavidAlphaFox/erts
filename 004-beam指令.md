#<center>BEAM指令</center>

Erts做为一个虚拟机，就一定需要有虚拟机的指令。Erts的虚拟指分为两种，一种是通用的指令，另一种是Erts真正执行的宏指令。

##执行模型
Erlang的虚拟机拥有多个虚拟积存器

	寄存器R0-R1024，常规寄存器，R0是快速寄存器。
	寄存器FR0-FR1024，浮点寄存器。
	寄存器IP(instruction pointer)，指令指针寄存器，是一个指向可执行BEAM指令的指针
	积存器CP(continuation pointer)，延续寄存器，是一个指向当前函数调用的返回地址的指针
	寄存器EP(stack pointer)，栈指针寄存器，是一个指向栈上最后一个推入的值的数据
	寄存器HTOP(heap top)，堆顶指针积存器，是一个指向堆上第一个数据的指针

Erlang的执行宏指令总是有一堆各种参数类型附加在后面，每个参数类型都有自己的含义。

	r 表示x寄存器的第0个元素
	x 表示x寄存器
	y 表示y寄存器即栈
	i 表示一个打标签的整数
	a 表示一个打标签的原子
	n 表示nil
	c 表示打标签的常量，例如整形，原子和nil
	s 表示打标签的源操作数，上面任何一个 tagged source; any of the above
	d 表示打标签的目标寄存器，r x y
	f 表示失败标签
	j 是‘f’或者‘p’
	e 表示export项目的指针
	L 表示标签（label）
	I 表示一个非打标签整数
	t 表示一个非打标签整数可以打包
	b 表示bif的指针
	A 表示数值
	P 表示tuple或stack的偏移字节数量
	Q 和'P'一样，但是可以打包
	h 表示一个字符
	l 表示浮点数寄存器
	q 表示任意一个term
	
##一些细节

Erts中的指令设计非常类似CISC而不是RISC。并且Erts中指令执行是使用C语言手工编写的线程级的解释器。	
Erts大约又150条通用指令,并使用窥孔最佳化技术将这150条通用指令优化为450条左右的宏质量。

##通用指令
	label
	func_info
 	int_code_end
 	call
 	call_last
 	call_only
 	call_ext
 	call_ext_last
 	bif0
 	bif1
 	bif2
 	allocate
 	allocate_heap
 	allocate_zero
 	allocate_heap_zero
 	test_heap
 	init
 	deallocate
 	return
 	send
 	remove_message
 	timeout
 	loop_rec
 	loop_rec_end
 	wait
 	wait_timeout
 	is_lt
 	is_ge
 	is_eq
 	is_ne
 	is_eq_exact
 	is_ne_exact
 	is_integer
 	is_float
 	is_number
 	is_atom
 	is_pid
 	is_reference
 	is_port
 	is_nil
 	is_binary
 	is_list
 	is_nonempty_list
 	is_tuple
 	test_arity
 	select_val
 	select_tuple_arity
 	jump
 	'catch'
 	catch_end
 	move
 	get_list
 	get_tuple_element
 	set_tuple_element
 	put_list
 	put_tuple
 	put
 	badmatch
 	if_end
 	case_end
 	call_fun
 	is_function
 	call_ext_only
 	bs_put_integer
 	bs_put_binary
 	bs_put_float
 	bs_put_string
 	fclearerror
 	fcheckerror
 	fmove
 	fconv
 	fadd
 	fsub
 	fmul
 	fdiv
 	fnegate
 	make_fun2
 	'try'
 	try_end
 	try_case
 	try_case_end
 	raise
 	bs_init2
 	bs_add
 	apply
 	apply_last
 	is_boolean
 	is_function2
 	bs_start_match2
 	bs_get_integer2
 	bs_get_float2
 	bs_get_binary2
 	bs_skip_bits2
 	bs_test_tail2
 	bs_save2
 	bs_restore2
 	gc_bif1
 	gc_bif2
 	is_bitstr
 	bs_context_to_binary
 	bs_test_unit
 	bs_match_string
 	bs_init_writable
 	bs_append
 	bs_private_append
 	trim
 	bs_init_bits
 	bs_get_utf8
 	bs_skip_utf8
 	bs_get_utf16
 	bs_skip_utf16
 	bs_get_utf32
 	bs_skip_utf32
 	bs_utf8_size
 	bs_put_utf8
 	bs_utf16_size
 	bs_put_utf16
 	bs_put_utf32
 	on_load
 	recv_mark
 	recv_set
 	gc_bif3
 	line
	
	