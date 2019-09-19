# Solr 面试题

## 1.solr 的了解

> solr 是基于 Lucene 的，主要用作全文检索;

## 2.与 ElasticSearch 的区别

+ es 基本是开箱即用，非常简单 ; Solr 安装略微复杂一丢丢;
+ Solr 利用 Zookeeper 进行分布式管理，而 Elasticsearch 自身带有分布式协调管理功能;
+ Solr 支持更多格式的数据，而 Elasticsearch 仅支持json文件格式；
+ Solr 官方提供的功能更多，而 Elasticsearch 本身更注重于核心功能，高级功能多由第三方插件提供；
+ Solr 在传统的搜索应用中表现好于 Elasticsearch，但在处理实时搜索应用时效率明显低于 Elasticsearch;
+ Solr 是传统搜索应用的有力解决方案，但 Elasticsearch 更适用于新兴的实时搜索应用

## 3.Solr 的优缺点

+ 优点
  + 有一个成熟的开发者社区;
  + 支持多种数据格式的索引;
  + 发展比较成熟、稳定;
  + 搜索海量历史数据时，速度非常快，毫秒级返回数据;

+ 缺点
  + 建立索引时，搜索效率下降，实时索引搜索效率不高;
