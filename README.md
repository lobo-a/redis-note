# redis-note

优点：1、丰富的数据结构
     2、基于内存，速度快
     3、数据持久化
     4、单线程模式，数据并发安全


分布式锁：
加锁：SET resource_name my_random_value NX PX 3000
解锁：【其中KEYS[1]为resource_name， ARGV[1]为 my_random_value】
	if redis.call("get",KEYS[1]) == ARGV[1] then
	    return redis.call("del",KEYS[1])
	else
	    return 0
	end