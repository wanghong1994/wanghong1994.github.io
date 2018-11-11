# MapReduce实现Join算法

#### reduce端实现Join算法
 * 1.文件格式要注意，否则有乱码
 * 2.创建一个接受完整数据的bean（既能存放order信息，又能存放goods）
 * 3.在map端接受不同文件的数据，根据是哪个文件向完整的bean中设置对应信息，没有的要设置默认值，不能为null，否则会造成空指针异常
  	这时候map的工作就结束了<goodsid,bean>要注意序列化
 * 4.这时候因为map端输出的key是goodsid所以传入的reduce数据已经帮我们合并了   <goodsid,[orderbean1,orderbean2,goodsbean]>
  	要将迭代器中的数据进行拆分成：goodsbean 与 [orderbean1,orderbean2]
  	我们只需要对orderbean的集合进行循环，将orderbean缺少的商品信息  通过goodbean进行补全 ，这样就得到了我们想要的完整的join之后的数据了，我们就可以输出了。
  	因为我们要使用的数据来自迭代器，所以要拿出来使用要进行深拷贝
 
 缺点：这种方式中，join的操作是在reduce阶段完成，reduce端的处理压力太大，map节点的运算负载则很低，资源利用率不高，且在reduce阶段极易产生数据倾斜
 
#### map端实现Join算法
 
#### map端join
##### 原理阐述
适用于关联表中有小表的情形；
可以将小表分发到所有的map节点，这样，map节点就可以在本地对自己所读到的大表数据进行join并输出最终结果，可以大大提高join操作的并发度，加快处理速度

##### 实现过程
 * 主表order正常处理，从表goods以缓存文件的形式读入到job中
 * 主表数据在map中处理后 缺少从表数据的完整数据
 * 就需要对存放了主表数据完整对象设置缺少的从表数据
 * 那从表的数据从哪来？->通过setup（）这个会在循环调用map前只执行一次的方法
 * 来对我们的缓存文件进行加载，将解析后的一个个存储了goods信息的对象以<外键，goods对象>的形式加入map中
 * 方便我们使用。这样在map中我们通过map.get(外键)就能取到我们当前这个order所对应的goods了，进行赋值并写入就行了