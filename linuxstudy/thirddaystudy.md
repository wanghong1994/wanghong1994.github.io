﻿## sed and awk
#### sed(行读取)
sed是一个很好的文件处理工具,本身是一个管道命令,主要是以行为单位进行处理,可以将数据行进行替换,删除,新增,选取等特定工作.
基本语法:
sed 选项 动作 filename
- 选项 -n
- 动作 -a   新增往上增加
	- i 往上一行添加
	- c 替换  1,5c会将这一块区域整个替换  不会每行都替换
	- d 删除
	- p 输出
	- s 替换经常配合正则进行操作
	- w 写入 sed 'w 要被写入的文件（目标文件）' 读取内容的文件 只要用w向文件中进行写入就会将目标文件之前的内容全部干掉
	- r 读取 sed '2r 要读取的文件' 加入数据的文件（目标文件）


- 高级操作
	- | 使用管道符配合其他命令
	- {} 可以让sed直行多个动作  只是动作间要用分号隔开
	- & 替换
		& 相当于占位符的作用  就是我们s/查询条件/ 查询到的内容
		可以在s/查询条件/要替换成的内容中进行查找 实现追加的效果
	- \u转成大写 可以配合我们的&来实现将匹配内容转成大写的操作
	- ()分组功能
	
- 怎么在sed中获取分组的内容呢?
首先分组的序号是从1开始的并且是按照从左到右的顺序排列
要获取使用\分组的序号来进行获取，列如\1就是个占位符

#### awk(行读取)
awk的基本格式:
awk options选项 'command' file
- NR,行号
- NF,列数
- $1 $n
- -F设置分割符 默认情况下是使用空格来进行切割
print
printf
要使用正则：~/正则匹配规则/
如果用!~就是对正则匹配内容取非
- awk的扩展格式
	- awk options选项 'BEGIN{} command END{}' file