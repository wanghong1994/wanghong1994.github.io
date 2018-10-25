# The Second Day Study Hadoop
## 伪分布式hadoop的安装

#### 1.创建新用户
#### 2.链接到虚拟机
#### 3.关闭防火墙
- systemctl disable firewalld 永久关闭
- systemctl stop firewalld 临时关闭
- systemctl status firewalld 查看防火墙状态
#### 4解压安装jdk.
- 解压：tar -zxf jdk-8u181-linux-x64.tar.gz
- 查看路径:
```
[hadoop@localhost ~]$ cd jdk1.8.0_181/
[hadoop@localhost jdk1.8.0_181]$ pwd
/home/hadoop/jdk1.8.0_181
```

- 配置环境变量
```
vim /etc/profile

export JAVA_HOME=/home/hadoop/jdk1.8.0_181
```

#### 5.解压安装hadoop
- 解压tar -zxf hadoop-2.7.3.tar.gz
- 查看路径:
```
[hadoop@localhost jdk1.8.0_181]$ cd ~/hadoop-2.7.3
[hadoop@localhost hadoop-2.7.3]$ pwd
/home/hadoop/hadoop-2.7.3
```

- 配置环境变量
```
vim /etc/profile

export HADOOP_HOME=/home/hadoop/hadoop-2.7.3
PATH=$PATH:$JAVA_HOME/bin:$HADOOP_HOME/bin:$HADOOP_HOME/sbin
```

#### 6.配置hadoop中的5个文件<configuration>
(1)hadoop-env.sh
```
vim hadoop-env.sh

[hadoop@localhost hadoop]$ echo $JAVA_HOME
/home/hadoop/jdk1.8.0_181
export JAVA_HOME=/home/hadoop/jdk1.8.0_181
```

(2)core-site.xml
```
vim core-site.xml

    <property>
        <name>hadoop.tmp.dir</name>
        <value>/home/hadoop/tmp</value>
    </property>
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://172.18.24.20:9000</value>
    </property>
```

(3)hdfs-site.xml: 
```
vim hdfs-site.xml 

    <property>
        <name>dfs.namenode.name.dir</name>
        <value>file:/home/hadoop/dfs/name</value>
    </property>
    <property>
        <name>dfs.datanode.data.dir</name>
        <value>file:/home/hadoop/dfs/data</value>
    </property>
```

(4)yarn-site.xml
```
vim yarn-site.xml 

    <property>
        <name>mapreduce.framework.name</name>
        <value>yarn</value>
    </property>

    <property>
        <name>yarn.nodemanager.aux-services</name>
        <value>mapreduce_shuffle</value>
    </property>
```

(5)mapred-site.xml（cp mapred-site.xml.templete）
```
cp mapred-site.xml.template mapred-site.xml
vim mapred-site.xml
    <property>
        <name>mapreduce.framework.name</name>
        <value>yarn</value>
    </property>
```

#### 7.格式化HDFS
- hadoop namenode -format
	- 看到Storage directory /home/hadoop/dfs/name has been successfully formatted.
	- 说明格式化HDFS
#### 8.启动HADOOP服务
```
start-all.sh
```

输入jps，连jps有6个说明你成功了
```
[hadoop@localhost hadoop]$ jps
3728 NameNode
3858 DataNode
4466 NodeManager
4024 SecondaryNameNode
4588 Jps
4174 ResourceManager
```
#### 9.关闭hadoop服务
```
Stop-all.sh
```

# day day up 


