# The Firstday Study Hadoop
## Hadoop安装
#### 安装配置JDK
- 将JDK文件解压，放到/usr目录下
```
[root@wang1 ~]$ mkdir /usr
[root@wang1 ~]$ mv jdk-8u101-linux-x64.tar.gz  /usr/
[root@wang1 usr]$ tar -xvf jdk-8u101-linux-x64.tar.gz
```

- 配置环境变量

```
[root@wang1 ~]$ vim /etc/profile
```

配置以下内容到文件中

```
export JAVA_HOME=/usr/jdk1.8.0_181
export CLASSPATH=$:CLASSPATH:$JAVA_HOME/lib/
export PATH=$PATH:$JAVA_HOME/bin
```

使改动生效命令

```
[root@wang1 ~]$ source /etc/profile
```

#### 解压并配置Hadoop
将压缩包放到hadoop1下

解压

```
[hadoop1@wang1 ~]$ tar -zxvf hadoop-2.7.3.tar.gz
```

配置环境变量

```
[hadoop1@wang1 ~]$ vim .bash_profile
```

配置以下内容到文件中

```
export HADOOP_HOME=/home/hadoop1/hadoop-2.7.3
PATH=$PATH:$HOME/.local/bin:$HOME/bin:$HADOOP_HOME/bin:$HADOOP_HOME/sbin
```

使改动生效命令

```
[hadoop1@wang1 ~]$ source .bash_profile 
```


#### 测试案例
默认情况下,Hadoop已经被配置到单节点模式,因此不需要在做额外的配置.

```
[hadoop1@wang1 ~]$ mkdir input  
[hadoop1@wang1 ~]$ cp etc/hadoop/*.xml input  
[hadoop1@wang1 hadoop-2.7.3]$ bin/hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.3.jar grep input output 'dfs[a-z.]+'  
[hadoop1@wang1 hadoop-2.7.3]$ cat output/*
```

输出结果为:
1	dfsadmin

那么单节点模式的Hadoop就已经安装完成！