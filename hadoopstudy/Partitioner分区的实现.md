# Partitioner分区的实现

#### 使用分区的步骤

- 1.设置job.setPartitionerClass
- 2.创建分区类，继承partitioner类
- 3.根据自己业务逻辑，通过key，value，count的操作

#### 实际需求
从log中获取手机号，上行流量，下行流量，总流量。
reduce之后输出的结果要手机号，流量对象（上行流量，下行流量，总流量）

#### 分析

要使用自定义的类型作为输出
- 1.要根据我们的数据进行建模（创建实体类）
- 2.mapper形参怎么写，map()方法中怎么对数据进行切割筛选
	将我们的数据放入自定义的bean中，想好将bean以key，还是value进行输出
- 3.map的结果最终要写入磁盘中，所有我们自定义的bean要支持序列化
	Serializable是java提供的重量级序列化 hadoop更建议用WritableComparable来实现序列化和反序列化
	这时候有write（）写入文件和readfields（）从文件中读取的方法需要我们实现
	否则在reduce阶段是得不到数据的，而且要注意的一点是readfields()方法中调用的read方法
	的时候一定要按照写入的顺序进行读取 对我们的属性值进行赋值，否则会错乱
- 4.reduce当中要注意形参和输出位置，以及在driver区	对应好我们reduce要输出的类型	
	job.setOutputKeyClass(Text.class);
	job.setOutputValueClass(StreamBean.class);
- 5.当我们处理好后，我们reduce后的结果就可以输出到我们指定的位置了
	但是要注意自定义bean的tostring（）方法的重写，否则输出也不会是我们想要的