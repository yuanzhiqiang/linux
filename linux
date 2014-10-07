一般模式

编辑模式：
"i"
"o"
"a"
命令行模式
":"----- 
	"w":保存 "q":退出  "set nu":显示行号  "dd":删除光标所在的一行 "u":撤销操作
	yy 复制当前行  yny 复制当前行开始 往下数n行  p  在当前行粘贴  dw 删除一个词  
	yw 复制一个词
	$ 移动到行尾
	^ 移动到行的首部
	G 到达最后一行
	1G 到第一行
	60G 到达第60行
	dG删除当前行到最后一行
	dnG删除当前行开始往下数n行
:%s/old/new/g 全部替换old替换为new

e! 重新读入文件

"?"----- 反查找 n查找上一个 N查找下一个  
"/"----- 正查找 n查找下一个 N查找上一个  




~:用户家目录  cd ~
-:上次所在的目录 cd -


d  目录
c  字符流
s   socket
p   管道文件
l   连接文件
b   设备文件

目录操作
	mkdir  rmdir
文件的查看 
	ls

别名:alias ll='ls -l'

命令目录、别名查看：which ll
使用原始命令：/bin/ls
	
复制 删除 移动  创建或修改
	cp mv rm touch
修改文件更新时间:touch -d/-t 1999/08/5s 
查阅
	cat tac(倒置) more(可分页查看,空格下翻页) less(上下箭头可用) head(从头查看多少行 head -3) tail(从尾部查看 -f:监测(日志)文件改变)	


文件与目录权限的意义与用法
作用到文件上：
	r:可以读
	w:可以修改  但不代表能删除该文件
	x:可以被系统运行(类似于.exe,.bat等格式的能被windows执行,包含x的权限才能被linux执行)
作用到目录上
	r:可以ls查看目录内的文件
	w:可以目录内创建、删除文件   重命名目录
	x:可以进入(cd)目录
	
     rwx                  r-x                 r-x
所属用户的权限       所属用户组的权限       其他权限(非所属用户、所属用户组)



文件属性操作的命令
	chown(可以替代chgrp):
		将1.txt文件的所属用户改为user：chown user 1.txt
		chown，命令修改文件所属组：chown .root 1.txt
		将文件拥有者和所属组一起修改：chown root:root 1.txt或chown root.root 1.txt
	chgrp：
		修改文件所属组：chgrp bbb 1.tx6t 
		递归修改目录的所属组：chgrp -R bbb TT 
	chmod：
		a:all   u:用户   g:组     o:orther
		将file1文件加上x执行权限chmod x file1(等价于chmod a+x file1)
		将file1文件所有者加上x执行权限chmod u+x file1(g、o类似)
		将file1文件所有者去除x执行权限chmod u-x file1(g、o类似)
		复合操作:chmod O+wx-r-wx,u+wx,g-x file1
		赋值操作:chmod o=rwx file1
		chmod 523 file1
	创建一个文件的默认权限:644(666 - umask值) umask默认值为022
	创建一个目录的默认权限:755(777 - umask值)
	修改umask(不建议):umask 222
	
	
	文件的特殊权限：
		Suid：
			限制:只能设置二进制可执行程序(目录和其他文件不行)
			功能:无论谁执行这个程序，linux都以程序的拥有者身份进入权限获取流程(passwd)
			chmod u +/- s 
			chmod 4777 + 二进制文件名
		Sgid:
			限制:可以作用在目录和二进制可执行程序
			功能:
				作用在二进制:与Suid相似,无论谁执行这个程序，linux都以程序的拥有者身份进入权限获取流程(passwd)
				作用在目录:默认情况下，用户建立文件，文件所属的组是主组
							如果在sgid目录下创建文件，则文件的所属组是继承目录的属组，新建立的目录业继承g+s的权限
			chmod g +/- s 
			chmod 2777 + 二进制文件名/目录
		sticky：
			限制:只能作用在目录上
			作用：任何人都可以在目录下建立文件，只有root和建立者本人可以删除文件
			chmod o+/-t 目录
			chmod 1777 +目录
	
	ACL(Access Control List:访问权限控制)权限设置:
		setfacl:设置某一些用户的特殊权限
				setfacl -m(设置权限) u:m1:rw testacl(文件名) 
				setfacl -b testacl 删除文件全部facl权限
				setfacl -m g:manager:rx tech/ hr/ 
		getfacl:获取某一些用户的特殊权限
				getfacl testacl(文件名) 
					# file: testacl
					# owner: root
					# group: root
					(拥有者权限)user::rw-
					(m1用户权限)user:m1:rw-
					(拥有者所属组权限)group::r--
					(文件的有效权限)mask::rw-
					(其他人权限)other::r--
		
		
		
		
磁盘分区与格式化：
	分区命令:fdisk + 分区目录
	查看当前分区信息 fdisk -l
		磁盘分区：fdisk /dev/sda
			写入后必须执行partprobe（刷新分区表）命令
	
	
	磁盘格式化：
		mkfs -t命令：mkfs -t ext3 /dev/sda5或mkfs.ext3 /dev/sda5
		
	磁盘挂载:mount /dev/sda5 /root/sda5/
	
	查看文件大小:df -a/-h
	
	磁盘卸载:umount /root/sda5
	
	开机自动挂载:vim /etc/fstab
	
	
内存交换空间的问题
SWAP

1. 安装linux的时候   忘记配置swap
2. swap不足    无法正常操作   1G

设置swap分区：
	方式一：
		步骤：
		1.使用fdisk开辟一个swap分区fdisk /dev/sda
		2.t 4 82(swap分区的id)
		3.partprobe（刷新分区表）
		4.swapon /dev/sda5
	方式二：
		步骤：
		1.创建一个100M左右的文件
			dd if=/dev/zero(0发射器) of=swap1(要产生文件的位置) bs=10(每次10M) count=10(10次)   
	
		2.将这个文件格式化成swap格式的文件
			mkswap swap1
		3.swapon swap1
		
磁盘配额(quota)：限制用户或者用户组 对硬盘的使用率 
	空间大小的配额
	文件数量的配额
	使用限制：
	只能针对于整个文件系统
	只针对分区 不针对目录
	内核 或 文件系统必须支持 quota   EXT3
	针对一般用户有效 root无效
	
	soft     hard
	  8       10
	  
	倒计时宽限时间  grace time
	如果超过了这个期限，soft限制会代替hard限制。
	
		
		
