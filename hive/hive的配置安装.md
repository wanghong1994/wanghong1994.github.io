# Hive,Mysql在Linux的配置安装

#### Mysql在Linux的配置安装
- 1.安装wget
	sudo yum -y install wget
- 2.下载mysql安装包
	wget http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm
- 3.安装mysql
	sudo yum -y install mysql
- 4.安装mysql服务
	sudo yum -y install mysql-server
- 5.安装软件
	sudo rpm -ivh mysql-community-release-el7-5.noarch.rpm
- 6.启动mysql
	systemctl start mysqld
- 7.登录mysql
	mysql -u root -p 默认没密码，让输密码直接回车就好

	
出现下面的图就说明mysql已经安装完成
![image.png](https://upload-images.jianshu.io/upload_images/14466054-14bbb45468ebba5f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### Hive在Linux的配置安装

- 1.下载hive安装包
- 2.解压安装包
	tar -zvxf 压缩包名字
- 3.配置环境变量
	vim /etc/profile
	
	export HIVE_HOME=/home/hadoop/apache-hive-1.2.1-bin
	在path后添加:$HADOOP_HOME/bin
	
	执行一下脚本文件
	source /etc/profile
	
- 4.执行hive命令看是否成功
出现下面的图就说明hive已经安装完成
![image.png](https://upload-images.jianshu.io/upload_images/14466054-b5220cbeef167f5a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 外置mysql
- 1.修改配置文件
	进入/apache-hive-1.2.1-bin/conf/目录下
	修改配置文件 vim hive-site.xml
	
	```
	<configuration>
		<property>
			<name>javax.jdo.option.ConnectionURL</name>
			<value>jdbc:mysql://127.0.0.1:3306/hivedb?createDatabaseIfNotExist=true</value>
		</property>
		<property>
			<name>javax.jdo.option.ConnectionDriverName</name>
			<value>com.mysql.jdbc.Driver</value>
		</property>
		<property>
			<name>javax.jdo.option.ConnectionUserName</name>
			<value>root</value>
		</property>
		<property>
			<name>javax.jdo.option.ConnectionPassword</name>
			<value>123456</value>
		</property>
	</configuration>
	```
	
- 2.下载jar包 mysql-connector-java-5.1.34
	上传到/home/hadoop/apache-hive-1.2.1-bin/lib下
	
- 3.配置远程访问
	设置远程访问数据库：
	登录后输入：
	mysql>GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'youmysqlpassword' WITH GRANT OPTION;
	mysql>FLUSH PRIVILEGES
	如果忘记密码：
	用命令编辑/etc/my.cnf配置文件，即：vim /etc/my.cnf 或者 vi /etc/my.cnf
	在文件中添加skip-grant-tables就可以免密登录

	service mysqld restart
	修改密码：
	UPDATE mysql.user SET authentication_string=PASSWORD('6757DUgu') where USER='root';
	MySQL> UPDATE mysql.user SET Password=PASSWORD('新密码') where USER='root’;
	MySQL> flush privileges;
	MySQL> exit
	
- 4.打开可视化工具进行连接
	可以连接就说明外置mysql已经配置完成

