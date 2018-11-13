# 自定义inputFormat和自定义outputFormat

#### 1.自定义inputFormat
- 1.1 需求
	无论hdfs还是mapreduce，对于小文件都有损效率，实践中，又难免面临处理大量小文件的场景，此时，就需要有相应解决方案

- 1.2 分析
	小文件的优化无非以下几种方式：
	- 1、在数据采集的时候，就将小文件或小批数据合成大文件再上传HDFS
	- 2、在业务处理之前，在HDFS上使用mapreduce程序对小文件进行合并
	- 3、在mapreduce处理时，可采用combineInputFormat提高效率

- 1.3 实现
	本节实现的是上述第二种方式
	程序的核心机制：
	自定义一个InputFormat
	改写RecordReader，实现一次读取一个完整文件封装为KV
	在输出时使用SequenceFileOutPutFormat输出合并文件
- 1.4 具体步骤
	* 以什么形式输入，这时候map形参要注意对应
	* 1.driver区进行设置 job.set
	* 2.创建自定义的iutputformat extends fileoutputformat
	* 3.实现对应的方法 -> recordreader（自定义）除了要创建对应的recordreader 
		还需要通过initialize（split， context）来进行赋值
	* 4.创建对应的recordreader extends recorderreader
	* 5.实现对应方法
 		1.initialize(InputSplit split, TaskAttemptContext context)
 		因为我们recordreader是真正要读数据的人，所以需要通过split来得到要读取的文件信息
  		从context.getConfiguration()方法获取到我们配置文件系统的位置
  		2.nextKeyValue()按格式读取文件 并根据读取的结果返回 返回值决定map是否要执行
  		3.getCurrentKey()map方法传入的key值是从这个方法中获取的
  		4.getCurrentValue()map方法传入的Value值是从这个方法中获取的
  		5.getProgress()获取进度的方法
		
		
#### 2.自定义outputFormat
- 2.1 需求
	现有一些原始日志需要做增强解析处理，流程：
	1、从原始日志文件中读取数据
	2、根据日志中的一个URL字段到外部知识库中获取信息增强到原始日志
	3、如果成功增强，则输出到增强结果目录；如果增强失败，则抽取原始数据中URL字段输出到待爬清单目录
- 2.2 分析
	程序的关键点是要在一个mapreduce程序中根据数据的不同输出两类结果到不同目录，这类灵活的输出需求可以通过自定义outputformat来实现

- 2.3 实现
	实现要点：
	1、在mapreduce中访问外部资源
	2、自定义outputformat，改写其中的recordwriter，改写具体输出数据的方法write()
	
- 2.3 具体实现步骤
 * 结果输出到哪，以什么形式输出
 * 1.driver区进行设置 job.set
 * 2.创建自定义的outputformat extends fileoutputformat
 * 3.实现对应的方法 -> recordwriter（自定义）
  		1.需要通过this.getoutputpath(job);拿到我们要输出的位置
  		2.根据输出目录创建对应的输出流 传给recordwriter
 * 4.创建对应的 recordwriter extends RecordWriter
 * 5.实现3个方法
 		1.带参构造用来接收输出流，知道要往哪些位置写
  		2.write方法能用来接收到最终要写入的内容，在这进行逻辑判断决定往哪个输出流进行写入
  		3.close方法用来关闭流，也是我们job的结束
