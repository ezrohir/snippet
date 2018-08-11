### YYCache
+ 数据结构上, YYCache 使用 dict 来存储 key wapper-value, 这么做主要是能快速访问.
+ 同时为了快读增删, 满足limit等业务需要, wapper-value 组织成一个双向链表.
+ 对于读写安全, 使用 互斥锁 pthread_mutex_lock 保证线程安全.
+ 以上仅真对 YYCache 中的 memory cache.


### RAC 中 takeUntil throttleQ
