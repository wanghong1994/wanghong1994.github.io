# Hive常用指令
#### 数据库、表的操作
- 创建数据库
	create database mydb;
	show databases;
- 查看现有的表:show tables;
- 查看表结构描述 desc student;
- 查询数据 ：select * from student;
- 导入数据：
	- 从HDFS中导入数据：
		load data inpath '/data.txt' into table student;
	- 从本地导入数据：
		load data local inpath '/usr/local/data.txt' into table student;
	
- 建表语句相关解释
	- CREATE TABLE 创建一个指定名字的表。如果相同名字的表已经存在，则抛出异常；用户可以用IF NOT EXISTS选项来忽略这个异常
	- EXTERNAL 关键字可以让用户创建一个外部表，在建表的同时指定一个指向实际数据的 路径（LOCATION），Hive 创建内部表时，会将数据移动到数据仓库指向的路径；若创建 外部表，仅记录数据所在的路径，不对数据的位置做任何改变。在删除表的时候，内部 表的元数据和数据会被一起删除，而外部表只删除元数据，不删除数据（经典面试问题）
	- PARTITIONED 在 Hive Select查询中一般会扫描整个表内容，会消耗很多时间做没必要的工作。有时候只需要扫描表中关心的一部分数据，因此建表时引入了partition概念。表可以拥有一个或者多个分区，每个分区以文件夹的形式单独存在表文件夹的目录下，分区是以字段的形式在表结构中存在，通过desc table命令可以查看到字段存在，但是该字段不存放实际的数据内容，仅仅是分区的表示。分区建表分为2种，一种是单分区，也就是说在表文件夹目录下只有一级文件夹目录。另外一种是多分区，表文件夹下出现 多文件夹嵌套模式
	- ROW FORMAT 	确定表的具体列的数据
	- STORED AS SEQUENCEFILE/TEXTFILE/RCFILE 如果文件数据是纯文本，可以使用 STORED AS TEXTFILE。如果数据需要压缩，使用 STORED AS SEQUENCEFILE
	- CLUSTERED BY 对于每一个表（table）或者分区，Hive可以进一步组织成桶，也就是说桶是更为 细粒度的数据范围划分。Hive也是针对某一列进行桶的组织。Hive采用对列值哈希，然后除以桶的个数求余的方式决定该条记录存放在哪个桶当中。把表（或者分区）组织成桶（Bucket）有两个理由：
		获得更高的查询处理效率,使取样（sampling）更高效
	- LOCATION 指定数据文件存放的hdfs目录
- 创建内部表
	create table mytable(
		id int, 
		name string) 
	row format delimited fields terminated by '\t' stored as textfile;

- 创建外部表
	create external table mytable2(
		id int, 
		name string)
	row format delimited fields terminated by '\t' location '/user/hive/warehouse/mytable2';
- 创建分区表
	create table mytable3(
		id int, 
		name string)
	partitioned by(sex string) row format delimited fields terminated by '\t'stored as textfile;
- 查询表分区
	show partitions mytable3;
- 查询分区表数据
	select * from mytable3;
	
#### 修改表
- 重命名表
	alter table student rename to student_mdf
	
- 增加/改变/替换列
	alter table student_mdf add columns (sex string);
	alter table student_mdf change sex gender string;
	alter table student_mdf replace columns (id string, name string);

- 删除表
	语法结构
	DROP TABLE [IF EXISTS] table_name;

#### 增加/删除分区
- 增加分区
	alter table mytable3 add partition(sex='unknown') localtion /user/hive/warehouse/mydb.db/mytable3/sex=unknown;
- 删除分区
	alter table mytable3 drop if exists partition(sex='unknown');

#### Insert 插入数据
- 插入一条数据
	insert into table student_mdf values('1','zhangsan');
- 注意
	动态分区默认情况下是没有开启的。开启后，默认是以”严格“模式执行的，在这种模式下要求至少有一列分区字段是静态的。这有助于阻止因设计错误导致查询产生大量的分区。但是此处我们不需要静态分区字段，估将其设为 nonstrict
	set hive.exec.dynamic.partition.mode=nonstrict;