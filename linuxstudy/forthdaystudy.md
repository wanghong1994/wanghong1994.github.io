
## Shell基础

#### shell基本格式
- 代码写在普通文本文件中，通常以.sh结尾
	- 例如：[root@master ~]# vim helloworld.sh
	
	```
	#!/bin/bash
	echo “hello world!”
	```

- 写完保存退出
注:脚本第一行是固定需要的,表明用哪一种shell解析器来执行我们的这个脚本程序.

#### shell执行方式
- sh方式
	- 例如：[root@master ~]# sh helloworld.sh
	- 此方式是直接指定用系统默认的bash shell解释执行
	
- source方式
	- source命令也称为“点命令”，也就是一个点符号（.）,是bash的内部命令
	- 使Shell读入指定的Shell程序文件并依次执行文件中的所有语句
	- source命令通常用于重新执行刚修改的初始化文件，使之立即生效，而不必注销并重新登录
	- 例如
	- [root@master ~]# . helloworld.sh
	
- 直接执行该脚本文件
	- 可以有两种方式，不过这两种方式的执行，都需要该文件有执行权限，所以在执行之前，我们要更改他的执行权限
	- 例如
	- [root@master ~]# chmod 755 helloworld.sh
	- [root@master ~]# ./helloworld.sh
	- [root@master ~]# /root/helloworld.sh
	- 注意:一定要写成 ./test.sh，而不是 test.sh，运行其它二进制的程序也一样，直接写 test.sh，linux 系统会去 PATH 里寻找有没有叫 test.sh 的，而只有 /bin, /sbin, /usr/bin，/usr/sbin 等在 PATH 里，你的当前目录通常不在 PATH 里，所以写成 test.sh 是会找不到命令的，要用 ./test.sh 告诉系统说，就在当前目录找。

## Bash基本功能
- 历史命令history
	- 简介
	- 在Bash中输入history指令可以查询用户的过往操作
	- 历史命令会默认保存1000条，可以在环境变量配置文件中/etc/profile进行修改
	- History表存储在内存中，在用户logout时会记录入用户家目录的.bash_history文件中，在下次login时载入
	- 选项
	- -c：清除历史命令
	- -w：把缓存中的历史命令写入历史命令保存文件  保存位置：~/.bash_history
#### 输入输出重定向
- 重定向操作	
	- 重定向输入	<	从指定的文件读取数据，而不是从键盘输入
	- 重定向输出	>	将输出结果保存到指定的文件（覆盖原有内容）
	- 重定向输出   >>	将输出结果追加到指定的文件
	- 标准错误输出	2>	将错误信息保存到指定的文件（覆盖原有内容）
	- 标准错误输出2>>	将错误信息追加到指定的文件中
	- 混合输出	&>	将标准输出、标准错误的内容保存到同一个文件中
	
- 管道符
	- 用法
	- 管道操作符号“|”
	- 将左侧的命令输出结果，作为右侧命令的处理对象
	- 格式
	- cmd1  |  cmd2  [... | cmdn]
	- 例如
	- [root@master ~]# cat test.txt | wc -l
	
- 通配符
	- * 代表 0 个到无穷多个任意字符 
	- ？ 代表一定有一个任意字符
	- [] 代表一定有一个在括号内的字符(非任意字符)。例如 [abcd] 代表一定有一个字符， 可能是 a, b, c, d 这四个任何一个 。
	- [ - ]若有减号在中括号内时，代表在编码顺序内的所有字符。例如 [0-9] 代表 0 到 9 之间的所有数字，因为数字的语系编码是连续的！
	- [^]若中括号内的第一个字符为指数符号 (^) ，那表示反向选择，例如 [^abc] 代表 一定有一个字符，只要是非 a, b, c 的其他字符就接受的意思
	
- 其他特殊符号
	- ‘ ’	单引号，在单引号中所有的特殊符号，如“$”和“·”（反引号）都没有特殊含义
	- “ ”	双引号，在双引号中特殊符号都没有特殊含义，但是“$”,”`”和”\”是例外，拥有“调用变量的值”、“引用命令”和“转义符”的特殊含义
	- · ·	反引号，反引号括起来的内容是系统命令，在Bash中会先执行它，和$()作用一样，不过推荐使用$(),因为反引号非容易看错
	- $()	和反引号作用一样，用来引用系统命令
	- #	在shell脚本中，#开头的行代表注释
	- $	用于调用变量的值，如果要调用变量name的值时，需要$name的方式得到变量的值
	- \	转义符，跟在\之后的特殊符号将失去特殊含义，变为普通字符，如\$将输出“$”符号，而不当做是变量引用
	
- 常用热键
	- Ctrl + d  输入已结束
	- Ctrl + c   键盘中断请求
	- Ctrl + s  暂停屏幕输出
	- Ctrl + q  恢复屏幕输出
	- Ctrl + l  清屏，相当于clear
	- Tab     自动补完命令行与文件名
	- Ctrl + u  删除当前光标前的所有字符
	- Ctrl + k  删除当前光标后的所有字符
	
- 截取命令
	- cut命令
	- 功能说明：显示文件中的某一列
	- 语法： cut  <选项>   文件
	- 常用选项
	- -d:指定分隔符
	- -f:依据 -d 的分隔字符将一段信息分割成为数段，用 -f 取出第几段的意思
	- -c:指定几个字符对应的列
	- 例如
	- 将PATH变量取出，找出第五个路径
	
	```
	[root@master ~]# echo $PATH | cut -d ':' -f 5 /usr/sbin
	```
	
	将PATH变量取出，找出第三和第五个路径
	
	```
	[root@master ~]# echo $PATH | cut -d ':' -f 3,5 /sbin:/usr/sbin
	```
	
## shell编程
#### Shell中的变量
显示当前shell中所有变量  :    set

- 系统变量
	- 通过set命令查看系统变量
	- 常用的系统变量:$PWD ,$SHELL ,$USER ,$HOME
- 自定义变量
	- 格式：变量名=变量值
	- 规则:
	- 变量与变量内容以一个等号来连结
	- 等号两侧不能有空格
	- 变量名以字母或下划线开头，区分大小写，建议全大写
- 特殊变量
	- $#：表示参数的个数，常用于循环
	- $*：参数的内容
	- $$：当前shell进程的pid值
	- $?：前一命令返回的状态值（0为正常）
	- $0 表示当前脚本名称
	- $1 第一个参数
	- $N 第N个参数

#### 运算符
- 算数运算
	- 格式：expr  变量1   运算符  变量2  [运算符 变量3] ...
	- 例如
	- 计算（2+3）x4的值
	- [root@master~]# expr `expr 2 + 3` \* 4
- 常用运算符
	- 加法运算：+
	- 减法运算： -
	- 乘法运算： \*
	- 除法运算： /
	- 求模（取余）运算： %
	
#### 控制流程
- if语句结构
	- 单分支结构
	示例:判断挂载点目录，若不存在则自动创建 
	```
	[root@master ~]# vim test1.sh
	
	#!/bin/bash
	MOUNT_DIR="/media/cdrom/"
	if [ ! -d $MOUNT_DIR ]
	then
		mkdir -p $MOUNT_DIR
	fi

	```
	
	- 双分支结构
	
	```
		#!/bin/bash
		read -p "please input your name:" NAME
		if [ $NAME = root ]
		then
			echo "hello ${NAME},welcome!"
		else
			echo "not any one,get out here!"
		fi

	```
	
- case语句结构
	- case语句结构
	- 示例：提示用户输入一个字符，判断出该字符是字母、数字或者其他字符
	- [root@master ~]# vim casetest.sh	
	
	```
	#!/bin/bash
	read -p "请输入一个字符，并按Enter键确认：" KEY
	case "$KEY" in
        [a-z]|[A-Z])
                echo "您输入的是字母"
                ;;
        [0-9])
                echo "您输入的是数字"
                ;;
        *)
                echo "您输入的是空格、功能键或其他控制字符"
	esac

	```
- case语句

```
格式
case $1 in
start)
	echo "starting"
	;;
stop)
	echo "stoping"
	;;
*)
	echo "Usage: {start|stop} “
esac
```

- 循环语句
- for语句结构	
	- for语句结构
	- 示例：批量添加用户：用户名存放在users.txt文件中，每行一个
	- [root@master ~]# vim users.sh
	```
	#!/bin/bash
	ULIST=$(cat /root/users.txt)
	for UNAME in $ULIST
	do
        useradd $UNAME
        echo "123456" | passwd --stdin $UNAME
	done

	```
	
	- for...do...done 的数值处理
	- 语法
	for (( 初始值; 限制值; 执行步阶 )) 
	do 
	程序段 
	done

	- 初始值：某个变量在循环当中的起始值，直接以类似 i=1 设定好
	- 限制值：当变量的值在这个限制值的范围内，就继续进行循环。例如 i<=100
	- 执行步阶：每作一次循环时，变量的变化量。例如 i=i+1
	
	```
	for ((i = 0; i <= 5; i++))
	do
		echo "welcome $i times"
	done
	```
	
- while语句的结构
	- 示例2：计算1到100数字之和
	- [root@master ~]# vim num.sh
	
	```
	#!/bin/bash
	read -p "Please input a number, I will count for 1+2+...+your_input:" nu
	s=0
	for ((i=1;i<=$nu;i=i+1))
	do
        s=$(($s+$i))
	done
        echo $s

	```
	
	- 打印9*9乘法表
	- [root@master ~]# vim num.sh
	
	```
	#!/bin/bash
	for((i=1;i<=9;++i))
	do
        for((j=1;j<=i;j++))
        do
                echo -ne "$i*$j=$((i*j))\t"
        done
        echo
	done

	```

#### Shell自定义函数
语法
```
[ function ] funname [()]
{
??? action;
??? [return int;]
}

function start()  / function start / start()
```
注意
1.必须在调用函数地方之前，先声明函数，shell脚本是逐行运行。不会像其它语言一样先预编译
2.函数返回值，只能通过$? 系统变量获得，可以显示加：return 返回，如果不加，将以最后一条命令运行结果，作为返回值。 return后跟数值n(0-255)

	
	
	
	
	
	
	