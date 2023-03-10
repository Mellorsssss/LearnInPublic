- 又称两阶段提交协议，分为prepare阶段和commit阶段。一个节点充当中心化的协调者，通知其他带数据节点是否需要提交（commit）或终止（abort）事务
	- prepare阶段中，协调者向所有参与节点发送prepare请求，如果收到所有人的同意回复则可以在下个阶段中进行提交，否则，在下个阶段中终止当前事务
	- commit阶段中，根据上一个阶段中做出的选择将需要执行的行为发送给所有参与节点
- 存在的问题
	- 单点故障。可以具体分为协调者crash以及参与者crash。
		- 协调者故障。显然，如果协调者在prepare之前crash，只需要保证其能够正常恢复；如果协调者在prepare之后并且完成信息收集之前crash，已经接收到了prepare请求的参与者节点将会阻塞并且保留自己已经申请的资源，此时即使协调者恢复，也可能丢失一些信息（可以通过持久化已经获取的信息避免这一问题）；如果协调者在prepare完成之后、commit完成之前crash，同样会出现部分参与者阻塞等待的问题，更为严重的是，如果协调者不知道自己之前做出的决策，可能会导致系统最后的状态产生不一致
		- 参与者故障。无论何时参与者发生故障，都可能导致协调者以及其他参与者阻塞，从协调者视角看它需要去收集参与者的prepare信息从而进入下一个阶段，同时其他参与者也会等待协调者下一个阶段的信息
- 解决方案
	- 可能的解决方案就是引入超时机制以及wal。协调者在prepare阶段可以通过超时来避免过长时间等待参与者，参与者的超时较为复杂，需要综合考虑其他节点的状态。wal可以保证持久化一些关键的中间数据。
	- 2pc+paxos：使用共识协议持久化每一个节点的投票选择，实际上就是完成了不同节点共享全局状态+wal。
	-