# ElastcSearch 面试题

## 1.ElasticSearch 的了解

> 一种基于 Lucene 的搜索引擎，它提供了一个分布式的、多用户的、具有 HTTP（超文本传输协议）Web 界面和无架构 JSON（JavaScriptObject Notation）文档的全文搜索引擎; 它是用 Java 开发的，是在 APACHE 许可下发布的一个开放源代码;

## 2.在并发情况下，Elasticsearch如果保证读写一致

+ 可以通过版本号使用乐观并发控制，以确保新版本不会被旧版本覆盖，由应用层来处理具体的冲突；
+ 另外对于写操作，一致性级别支持 quorum/one/all，默认为 quorum ，即只有当大多数分片可用时才允许写操作; 但即使大多数可用，也可能存在因为网络等原因导致写入副本失败，这样该副本被认为故障，分片将会在一个不同的节点上重建;
+ 对于读操作，可以设置 replication 为 sync(默认)，这使得操作在主分片和副本分片都完成后才会返回；如果设置 replication 为 async 时，也可以通过设置搜索请求参数 _preference 为 primary 来查询主分片，确保文档是最新版本
