### 运维篇

性能查询

ceph daemonperf mds.*

配置修改

ceph tell mds.* config set mds_cache_memory_limit 17179869184

配置查询

ceph daemon mds.* config show|grep mds_cache_memory_limit 

查询MDS整体状态

ceph fs status

