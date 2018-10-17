## The firstday study Linux
#### linux introduction
 Linux系统出现于1991年,芬兰大学大学生李纳斯(Linus Torvalds)和后来加入的众多爱好者共同开发完成.Linux是一个自由软件,是源代码开放的Unix.
###### 优良特性:
* 分时的多用户,多任务操作系统
* 多数网络协议支持,方便的远程管理
* 强大的内存管理和文件系统管理
* 大量的可用的软件和免费的软件
* 优良的稳定性和安全性
* 良好的可移植性和灵活性
* 可供选择的厂商多

###### Linux常见的发行版本
* RedHat Linux
* Fedora
* CentOS
* SuSE Linux
* Ubuntu Linux
* Mandrake Linux
* Caldera Linux
* Turbolinux
* Debian GNU/Linux
* Gentoo Linux
* Linpus Linux

###### Linux操作系统结构
![图片1.png](https://upload-images.jianshu.io/upload_images/14466054-1a742fe2a95d84e2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### Windows虚拟化技术开启
![图片2.png](https://upload-images.jianshu.io/upload_images/14466054-8a9e91b9b0eaa45a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
遇到上诉问题的解决方法:
* 首先确保自己的电脑主机开启了支持虚拟化技术,具体实现根据自己笔记本的型号配置
* 按住F2键进入Bios设置界面,首先看到的是main(概要)选项卡
* 选择进入Advanced高级—CPU Configuration  处理器设置
* 找到Intel Virtualization Technology英特尔虚拟化技术选项
* 设置为Enabled开启,再F10保存退出即可

#### linux目录结构
![QQ图片20181017195151.png](https://upload-images.jianshu.io/upload_images/14466054-e2cafdfdb623ebc7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### Linux系统的重启与关机
* reboot
* shutdown -r now 立刻重启(root用户使用)
* shutdown -r 10 过10分钟自动重启(root用户使用)
* shutdown -r 20:35 在时间为20:35时候重启(root用户使用)
* 如果是通过shutdown命令设置重启的话,可以用shutdown -c命令取消重启

* halt 	立刻关机
* poweroff 	立刻关机
* shutdown -h now 	立刻关机(root用户使用)
* shutdown -h 10 	10分钟后自动关机

#### 网络配置

###### 修改主机名
临时修改
```
[root@localhost ~]# hostname
localhost.localdomain
[root@localhost ~]# hostname lanou 
[root@localhost ~]# hostname 
[root@lanou ~]#
```
永久修改
* /etc/hostname文件
* 用途:保存全局网络设置,主要包括主机名信息
* lanou     //设定主机名

###### ping命令
* 测试网络连通性
* 格式:ping [选项] 目标主机
```
[root@localhost ~]# ping 192.168.4.110
PING 192.168.4.110 (192.168.4.110) 56(84) bytes of data.
64 bytes from 192.168.4.110: icmp_seq=1 ttl=128 time=0.694 ms
64 bytes from 192.168.4.110: icmp_seq=2 ttl=128 time=0.274 ms
……
```

###### 查看网络接口信息
* 查看所有活动网络接口的信息
* 执行 ifconfig命令
* 查看指定网络接口信息
* 格式:ifconfig	网络接口名
* Ifconfig不能用,使用yum命令 
* yum install net-tools

###### 虚拟机网络配置图
![图片3.png](https://upload-images.jianshu.io/upload_images/14466054-7704e7ae850813cf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### 设置防火墙
* 查看防火墙状态
* service firewalld status
* centos7关闭防火墙
* //临时关闭
* systemctl stop firewalld
* //禁止开机启动
* systemctl disable firewalld

###### 本地主机映射文件
* /etc/hosts 文件
* 用途:保存主机名与IP地址的映射记录
```
[root@localhost ~]# cat /etc/hosts
127.0.0.1		localhost.localdomain  localhost
......
119.75.218.70	 www.baidu.com
```
![图片4.png](https://upload-images.jianshu.io/upload_images/14466054-450135847156f37f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### 设置SELinux
* 查看SElinux,可能返回的结果有三种
* Enforcing:强制模式,代表记录安全警告且阻止可疑行为
* Permissive:宽容模式,代表记录安全警告但不阻止可疑行为
* Disable:关闭
* 当前有效
setenforce	[ Enforcing \ Permissive\ 1\ 0 ]
该命令可以立即改变SELinux运行状态,在Enforcing 和Permissive  之间切换,关机重启之后失效.
* 永久有效
修改配置文件/etc/selinux/config,将SELINUX=enforcing修改为SELINUX=disabled重启生效

#### 熟悉Linux基础命令
###### Linux命令的基本格式
* Linux命令的通用命令格式
* 命令字  [选项]  [参数]
* 选项及参数的含义
* 选项:用于调节命令的具体功能
* 参数:命令操作的对象,如文件目录名等

* ls:显示文件和目录列表(list)
* 常用参数:
* -l (long)
* -a(all)         注意隐藏文件 特殊目录.和..   
* -t	(time)

###### Linux的命令帮助
* 内部命令:属于Shell解析器的一部分
cd 切换目录(change directory)
pwd 显示当前工作目录(print working directory)
help 帮助
* 外部命令:独立于Shell解析器之外的文件程序
ls 显示文件和目录列表(list)
mkdir 创建目录(make directoriy)
cp 复制文件或目录(copy)
* 查看帮助文档
内部命令:help + 命令(help cd)
外部命令:man + 命令(man ls)

###### 使用命令管理文件和目录
* 目录操作命令
pwd cd ls mkdir du
* 文件操作命令
touch file cp rm mv which find
* 文件内容操作命令
cat more less head tail wc grep
* 压缩命令
gzip bzip2 tar

###### 目录操作命令
* pwd命令
用途:查看工作目录(Print Working Directory)
* cd命令
用途:切换工作目录(Change Directory)
格式:cd   [目录位置]
* ls命令
用途:列表(List)显示目录内容
格式:ls	[选项]...  [目录或文件名]
常用命令选项
-l :详细信息显示
-a:显示所有子目录和文件的信息，包括隐藏文件
-A:类似于“-a”,但不显示“.”和“..”目录的信息
-R:递归显示内容

####### 文件操作命令
* touch命令
用途:新建空文件，或更新文件时间标记
格式:touch	文件名
* file命令
用途:查看文件类型
格式: file   文件名
* cp命令
用途:复制(copy)文件或目录
格式:cp   [选项]    源文件或目录…   目标文件或目录
常用命令选项
-r:递归复制整个目录树
-p:保持源文件的属性不变
-f:强制覆盖目标同名文件或目录
-i:需要覆盖文件或目录时进行提醒
* rm命令
用途:删除(Remove)文件或目录
格式:rm   [选项]   文件或目录
常用命令选项
-f:强行删除文件，不进行提醒
-i:删除文件时提醒用户确认
-r:递归删除整个目录树
* mv命令
用途:移动(Move)文件或目录—— 如果目标位置与源位置相同,则相当于改名
格式:mv   [选项]...   源文件或目录...  目标文件或目录























