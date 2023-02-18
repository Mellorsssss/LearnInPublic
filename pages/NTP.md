- 网络时间协议，CS架构，客户端通过向NTP服务器请求以获得精准时间
- 时间校准
	- 流程
		- NTP客户端记录发送时间请求时间$$t_1$$，NTP服务器一般会返回接收请求时间以及返回请求时间$$t_2, t_3$$，NTP客户端记录接收NTP服务器回复时间$$t_4$$
		- 往返时间延迟（round-trip delay）
			- $$\delta = (t_4 - t_1) - (t_3 - t_2)$$
			-
		- NTP客户端接收到回复时的NTP服务器时间估计
			- $$t_3 + \frac{\delta}{2}$$
		-
		- 基于NTP客户端本地时间以及估计的NTP服务器时间，可以进行时钟校准：
			- 如果两者相差较小，NTP客户端通过调整ppm来保证NTP客户端以及NTP服务器时钟频率一致
			- 如果两者相差较大，NTP客户端直接**跳跃**至估计的NTP服务器时间
			- 如果两者相差特别大，则直接panic