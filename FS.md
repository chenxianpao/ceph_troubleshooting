#### Client *name* failing to respond to cache pressure(1 clients failing to respond to cache pressure)

ref: https://docs.ceph.com/en/latest/cephfs/cache-configuration/

Clients maintain a metadata cache. Items (such as inodes) in the client cache are also pinned in the MDS cache, so when the MDS needs to shrink its cache (to stay within `mds_cache_memory_limit`), it sends messages to clients to shrink their caches too. If the client is unresponsive or buggy, this can prevent the MDS from properly staying within its cache limits and it may eventually run out of memory and crash. This message appears if a client has failed to release more than `mds_recall_warning_threshold` capabilities (decaying with a half-life of `mds_recall_max_decay_rate`) within the last `mds_recall_warning_decay_rate` second.

客户端维护元数据缓存。 客户端缓存中的项目（例如inode）也固定在MDS缓存中，因此当MDS需要缩小其缓存（以保持在mds_cache_memory_limit内）时，它也会向客户端发送消息以缩小其缓存。 如果客户端无响应或有错误，则可能会阻止MDS正确地保持在其缓存限制内，并且最终可能耗尽内存并崩溃。 如果客户端在最后的mds_recall_warning_decay_rate秒内未能释放超过mds_recall_warning_threshold的功能（以mds_recall_max_decay_rate的半衰期衰减），则出现此消息。

1. ceph tell mds.0 cache drop （实测可用，其他未试）

   or

2. client重新挂载

   or

3. client evict

   例子，找到具体某个客户端，驱逐，再加回来。

   ceph tell mds.0 client ls

   ceph tell mds.0 client evict id=2519607 

   ceph osd blacklist ls

   ceph osd blacklist rm 172.20.39.33:0/2544833261



