- 核心思想
	- 假设绝大多数事务都是较短的，并且可以执行成功
- 阶段
	- 读阶段
		- 对于读/写的每一个对象，都是当前数据库中的一个对象副本
	- 验证阶段
		- 分为前向验证和后向验证
		- 以前向验证为例，需要保证：
			- 要么当前的事务在未提交事务开始之前完成写阶段。很明显，满足可串行化调度
			- 要么当前事务在未提交事务的写阶段之前完成，并且当前的事务写阶段中涉及的对象与未提交的事务中的读阶段中的对象没有交集
			- 要么当前事务的读阶段在未提交事务的读阶段之前已经完成，并且没有写任何未提交事务读阶段中会读取的值
	- 写阶段
		- 将私有空间中的所有值真正写入到数据库中
- 优点
	- 对于低冲突的场景，表现很好
	-
- 缺点
	- 需要大量的数据拷贝
	- 时间戳授时是一个瓶颈
	-