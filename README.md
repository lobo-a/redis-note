# redis-note

优点：1、丰富的数据结构
     2、基于内存，速度快
     3、数据持久化
     4、单线程模式，数据并发安全

单个redis所能承载的qps一般是10w级的，但是微博项目中以2w qps做资源评估

redis的客户端连接数应该按机器的来算，理论上受限于机器的句柄数量限制


分布式锁：
加锁：SET resource_name my_random_value NX PX 3000
解锁：【其中KEYS[1]为resource_name， ARGV[1]为 my_random_value】
	if redis.call("get",KEYS[1]) == ARGV[1] then
	    return redis.call("del",KEYS[1])
	else
	    return 0
	end