# 分组功能GroupingComparator的实现

#### 实现步骤

 要创好自定义的分组逻辑类
- 1）创建一个构造函数在内部调用super（要进行分组比较的类.class，true）
- 2）注意这里要进行比较的类必须去实现Comparable
 	因为我们分组比较在sort排序之后，而且只能对相邻的两个对象进行比较
 	所以我们要在实体类的compareto方法中将要进行分组的条件作为我们排序的第一要素，只有这样才能保证相同的属性相邻
	如果想进行排序，从第二要素开始排
- 3）根据我们要进行分组的逻辑实现抽象方法
	public int compare(WritableComparable a, WritableComparable b) 
	如果返回0就会认为是改进一个reduce
	对相邻的两个对象进行比较，如果返回0就会认为是该进一个reduce
	但不会立刻调用reduce，会继续进行下一轮比较
	直到如果比较结果不为0了，知道不是一个reduce了，这时候将之前的所有相同的放入一个reduce中
	如果想在reduce中获取到这些被认为该进一组的bean ，只要循环迭代器，在迭代器中的key就是每一个bean
	当一个reduce执行完，会继续执行我们的分组比较，遇到不同的再去执行reduce，从而形成一个循环，一直到我们reduce循环结束