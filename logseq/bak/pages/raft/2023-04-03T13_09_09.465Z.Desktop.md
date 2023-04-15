- 基础
- 优化
  collapsed:: true
	- prevote
	  collapsed:: true
		- [[动机]]：发生网络分区故障时，follower触发超时不断发起选举并递增term。当网络分区故障恢复时，follower的term可能大于当前leader的term，将会产生1次不必要的选举：当前follower由于logs往往远远旧于leader的logs，无法成为leader，只有等到下一轮超时时qurom中的节点重新成为leader。毫无疑问，两次失败的选举给系统带来了不必要的抖动。
		- 思路：在candiate发现自身无法成为leader时不更改term，从而避免term“过度膨胀”的问题。由于candiate发现自身是否可以成为leader依然需要通过RequestVote RPC（不过不会发生真正的投票），该技术被称作prevote
-