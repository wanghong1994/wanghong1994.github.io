# MR程序运行流程
- 1.mapreduce启动 先启动MRAppMaster，MRAppMaster根据本次job信息计算需要maptask数量，
然后申请启动相应数量的maptask
- 2.maptask启动后
	- a:利用inputformat调用recordreader读取数据，形成输入key value对
	- b:将键值对传入map()方法，并且把map方法输出的KV对收集到缓存
	- c:将缓存中的KV对按照K分区排序后不断溢写到磁盘文件
- 3.maptask进程任务结束后，MRAppMaster3、启动相应数量的reducetask进程，并告知reducetask进程要处理的数据范围（数据分区）。
- 4.Reducetask进程启动，根据MRAppMaster告知的待处理数据所在位置，从若干台maptask运行所在机器上获取到若干个maptask输出结果文件，在本地
合并排序，把相同key的kv归为一组，调用reduce方法进行运算，收集运算输出结果kv，调用outputformat方法将结果输出到外部存储
![image.png](https://upload-images.jianshu.io/upload_images/14466054-2112849821b89ac3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
#### mapTask并行度的决定机制
一个job的map阶段并行度由客户端在提交job时决定
而客户端对map阶段并行度的规划的基本逻辑为：
将待处理数据执行逻辑切片（即按照一个特定切片大小，将待处理数据划分成逻辑上的多个split），然后每一个split分配一个mapTask并行实例处理

这段逻辑及形成的切片规划描述文件，由FileInputFormat实现类的getSplits()方法完成，其过程如下图：
![image.png](https://upload-images.jianshu.io/upload_images/14466054-449a5a3fa1e4b792.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# mapreduce的shuffle机制（map阶段处理的数据如何传递给reduce阶段）
就是将maptask输出的处理结果数据，分发给reducetask，并在分发的过程中，
对数据按key进行了分区和排序。
- 1、分区partition
- 2、Sort根据key排序
- 3、Combiner进行局部value的合并
#### 详细过程
- 1、maptask收集我们的map()方法输出的kv对，放到内存缓冲区中
- 2、从内存缓冲区不断溢出本地磁盘文件，可能会溢出多个文件
- 3、多个溢出文件会被合并成大的溢出文件
- 4、在溢出过程中，及合并的过程中，都要调用partitoner进行分组和针对key进行排序
- 5、reducetask根据自己的分区号，去各个maptask机器上取相应的结果分区数据
- 6、reducetask会取到同一个分区的来自不同maptask的结果文件，reducetask会将这些文件再进行合并（归并排序）
- 7、合并成大文件后，shuffle的过程也就结束了，后面进入reducetask的逻辑运算过程（从文件中取出一个一个的键值对group，调用用户自定义的reduce()方法）
![image.png](https://upload-images.jianshu.io/upload_images/14466054-a4f64ce6c5d4290e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)