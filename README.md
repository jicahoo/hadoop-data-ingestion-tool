# hadoop-data-ingestion-tool



# 目标
* 通过阅读这个材料，读者能够了解到
    * 在大数据平台上，有哪些开源的OLAP解决方案和各自的优缺点。
    * 如何将数据导入到大数据平台（主要是Hadoop)

# 什么是OLAP
* 对多维数据的，多角度地交互式分析
* 属于广义BI的一部分
* 包含关系型数据库，报表，数据挖掘
* OLAP的核心概念是OLAP Cube，也称为多维Cube或HyperCube
* 和OLTP相对
* OLAP系统的分类：MOLAP, ROLAP, HOLAP

# 开源的大数据OLAP系统

* Apache Drill
  * Schema-free SQL Query Engine for Hadoop, NoSQL and Cloud Storage
  * 支持很多种数据源：HBase, MongoDB, MapR-DB, HDFS, MapR-FS, Amazon S3, Azure Blob Storage, Google Cloud Storage, Swift, NAS and local files
  * Drill supports the ANSI standard for SQL.
  * 编程语言：Java
* Apaceh Impala
  * Shipped by Cloudera, MapR, Amazon, Oracle
  * 目标：Do BI-style Queries on Hadoop
  * MPP架构，与Apache HAWQ类似。
  * 编程语言：C++为主
* Apache Kylin
  * 由eBay创立，很多成功的用户案例，百度地图，美团，北京移动，魅族，京东等
  * PB级别，最早是基于Hadoop的，据说，后期版本支持更多的大数据存储系统。
  * 支持SQL语言
  * 用户要设计Cube。设计好Cube之后，Kylin会按照Cube定义来构建Cube。构建Cube的数据源是Hadoop, 构建出的Cube，会存储到HBase.
  * 编程语言：Java
  * ​
* Apache Phoenix
  * 在能够满足OLTP应用的同时，满足分析任务（支持复杂的查询操作）
  * 基于HBase， 支持ANSI SQL和ACID。和Hadoop系列产品有较好的集成：Spark, Hive, Pig, Flume, and Map Reduce
  * 用户案例很多：Dell, Intel, 淘宝网，搜狗，华为。
  * 编程语言：Java
* Druid
  * 支持交互式查询，速度在亚秒级
  * 分布式的，面向列的，高性能的数据存储(data store)
  * 部分设计思想来自Goolge的BigQuery/Dremel/PowerDrill
  * 编程语言：Java
* Greenplum
  * Greenplum数据引擎是为新一代数据仓库和大规模分析处理而建立的软件解决方案，其最大的特点是不需要高端的硬件支持仍然可以支撑大规模的高性能数据仓库和商业智能查询。
  * 在数据仓库、商业智能的应用上，尤其在海量数据的处理方面Greenplum表现出极其优异的性能。
  * EMC收购的产品，但已完全开源，现在是EMC的子公司Pivotal在推动。
  * Greeplum是MPP架构，基于PostgreSQL
  * 无论是交互式分析还是批量模式的分析，都能很好地处理
  * 编程语言：C/C++
* HAWQ:
  * Pivotal公司将Greenplum验证过的成功技术引入到Hadoop，做了一个MPP架构的，运行在Hadoop上的SQL引擎
  * 查询性能上还是弱于Greenplum，但是仍然要比其他的SQL-Engine-On-Hadoop系统表现的要好。
  * ANSI SQL兼容: SQL-92, SQL-99, SQL-2003, OLAP extension; 支持ACID
  * 编程语言：C/C++
* Opentsdb
  * 分布式的，可伸缩的，时间序列数据库。 TSDB -> Time Series Database.
  * 基于HBase，专注于计算机系统的监控数据搜集：网络，操作系统，应用。
* Pinot (LinkedIn):
  * A realtime distributed OLAP datastore.
  * 适合于不可变的，仅会追加的数据(immutable append-only data)；而且要求从事件发生到对应数据可查询之间的延时必须要很短，这样的场景适用Pinot.
  * 面向列的，支持SQL
  * LinkedIn将它用于构建可伸缩的低延时的实时分析系统。
  * Pinot既可以消费离线数据源（Hadoop或者普通文件），也可以消费在线数据源（Kafka)
  * 编程语言：Java
* Presto:
  * 由Facebook创建
  * 是一个分布式查询引擎，可以支持很多数据源：Hive, Cassandra, 关系型数据库。
  * 查询时间：亚秒到分钟。
  * 数据规模：GB到 PB
  * 编程语言：Java
* Spark SQL:
  * 并不是大数据的OLAP：只是为了在Spark程序中，以统一的SQL的形式访问一些数据(Hive, Avro, Parquet, ORC, JDBC)，目标并不是OLAP



# 大数据的ETL工具
* TO: 完善
* 关注点：
  * 支持的数据源和数据目标
    * MongoDB -> Hive ?
  * 速度如何
  * 是否支持全量和增量的同步方式
  * 监控，调度，管理功能如何
  * ​
* Sqoop
  * Incremental copy data from RDBMS to HDFS?
  * Sqoop support converters?
* DataX

# 业务数据到数据仓库
* 范围
   * 从服务器硬件，到应用平台，到数据库搭建。估计需要补少人力物力。

* 业务数据

   * 业务数据的类型： 耗电（无修改）， 其他？以耗电数据为例子，做个初步架构，数据的流动从MySQL到数据展示页面，到归档，完整的生命周期。
   * 还有什么其他数据类型？
   * MySQL, Redis
   * 一天一千万条
   * 其他
* 如何导入到数据仓库
   * 不影响业务系统
   * ETL
   * RabbitMQ
   * 增量
   * 限流
   * kafka
   * RabbitMQ
   * kettle
   * https://www.cnblogs.com/DataPipeline2018/p/9414825.html 规则引擎的概念，规则定义数据以什么样的方式导入到数据仓库
   
* 数据仓库
   * 目标，可视化，交互分析，报警？
   * PostgreSQL? Roll up
   * Cassandra? 写入速度足够快？ 还是从Kafka直接到Postgres.
   * Greenplum
   * Apache Kylin
   * 时间序列数据
   * 地理位置数据
   
 * 从最终价值角度思考
   * 我也要从这个角度思考所有相关系统的一切，不然，你的系统就不会满足最终目标。
   * 推销敏捷开发，因为他们都不懂这个。选取一个具体的端到端的用户价值，开始项目。
   * 数据可视化工具: 
* 选型
   * Cassandra不是一个合适的数据仓库和商业智能系统：https://www.quora.com/Is-there-any-known-project-using-Apache-Cassandra-to-develop-data-warehousing-or-business-intelligence-systems
   * DataStax说可以用Cassandra做数据仓库：https://www.slideshare.net/VictorCoustenoble/bi-reporting-and-analytics-on-apache-cassandra
   * 数据可视化工具: 一个
   * 数据可视化工具: 
* 类似的系统
   * http://ajilius.com/doc/build-warehouse/
* 参考
   * https://www.metabase.com/blog/which-data-warehouse-to-use/
   
# 后面的章节不重要。



# Kylin

- 大数据平台上的OLAP
- Kylin: 美团对大数据量OLAP的点评： https://zhuanlan.zhihu.com/p/27461561


- https://blog.bcmeng.com/post/kylin-cube.html Kylin Cube的构建原理
- http://www.infoq.com/cn/articles/apache-kylin-algorithm Kylin Cube构建的新旧算法对比：逐层Cubing和Fast Cubing.

# Kylin案例
* 百度地图：http://www.infoq.com/cn/articles/practis-of-apache-kylin-in-baidu-map
* 链家(A+)：http://dataunion.org/27984.html
* 唯品会(A+) (Presto+Kylin)(前面的版本页面噪音少）：http://www.uml.org.cn/bigdata/201703092.asp http://www.infoq.com/cn/articles/application-of-apache-kylin-in-vip-big-data 
* 魅族(资料比较新）：https://mp.weixin.qq.com/s/BjL-v7_7lYAGNgEd3dQJyg
* 创始人采访：https://baijia.baidu.com/s?old_id=544791

# Reference
* https://coderwall.com/p/kgrwwq/sqoop-data-transfer-tool-from-rdbms-to-hadoop-box
* OLAP Benchmark 工具: http://www.tpc.org/default.asp


* Apache Kylin: https://share.iclient.ifeng.com/news/shareNews?forward=1&aid=109568477&aman=&gud=#backhead
* Apache Kylin 综述： https://www.jianshu.com/p/7fafa9103252
* Kylin. Presto的雷达图。https://www.iteblog.com/archives/1710.html
* PB-Level data analysis:   http://e.huawei.com/us/products/cloud-computing-dc/cloud-computing/bigdata/fusioninsight-libra
* Legacy Database: http://agiledata.org/essays/legacyDatabases.html
* Diff between Sqoop&Flume (Coupons use sqoop.)https://www.dezyre.com/article/sqoop-vs-flume-battle-of-the-hadoop-etl-tools-/176
* The tool of data ingestion to Hadoop: https://www.predictiveanalyticstoday.com/data-ingestion-tools/
* Demo很酷 Oralce到Hadoop: http://discover.attunity.com/replicate-express-registration.html
* Attunity as the Hadoop data ingestion tool: https://www.attunity.com/hadoop-data-ingestion-tool/ 

