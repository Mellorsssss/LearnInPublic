- 算法
	- 从main method开始遍历，对于每一个method中的所有call site，使用前文给出的resolve方法获取对应的m，并添加cs->m边到call graph中。以此法遍历所有可达的method。
- 影响精度的因素
	- 使用[[CHA]]或者[[指针分析]]