# hadoop在windoes下的安装配置

#### 1.准备hadoop-2.7.3安装包，hadooponwindows-master

#### 2.将hadooponwindows-master文件夹下的bin和etc文件夹替换hadoop-2.7.3下的bin和etc文件夹

#### 3.把bin下的hadoop.dll和winutils复制的C:\Windows\System32下

#### 4.配置hadoop环境变量

	- (1)添加系统变量HADOOP_HOME=F:\hadoop-2.7.3\hadoop-2.7.3
	- (2)编辑PATH变量，新建%HADOOP_HOME%\bin 新建%HADOOP_HOME%\sbin
	- (3)保存
	
#### 5.编辑F:\hadoop-2.7.3\hadoop-2.7.3\etc\hadoop下的hadoop-env.cmd文件

	- set JAVA_HOME=C:\PROGRA~1\Java\jdk1.8.0_131
	- 注意要把C:\Program Files\Java\jdk1.8.0_131中的Program Files改成PROGRA~1再保存。
	
#### 6.在cmd中输入指令hadoop和hadoop -version查看配置是否正确

#### 7.正确后，在配置F:\hadoop-2.7.3\hadoop-2.7.3\etc\hadoop下的hdfs-site.xml文件

	- 输入namenode和datenode要存储的路径如F:\data\namenode 和 F:\data\datanode
	
#### 8.在cmd中输入hadoop namenode -format 初始化namenode 注意要初始化成功(successfully)

#### 9.在cmd中输入start-all.cmd，等执行完毕后输入jps查看namenode、datanode是否启动，也可在浏览器中输入localhost:50070查看是否成功

### 注意：
	- (1)若找不到jps命令，说明jdk没有配置好
	- (2)若成功格式化后发现namenode、datanode起不来，可以查看报错信息，看看端口是否被占用，若被占用可自行百度查看Windows怎么结束占用进程，结束进程后先关闭stop-all.cmd，再启动试试看. 