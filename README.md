# hadoop-data-ingestion-tool
How to load data from other system/application to hadoop


# Goal
* A tool for sync data from different data systems to an identical data system, in order to do data analysis. The data volume is PB-level.
    * Maybe to Hive, Cassandra, PostgresSQL and so on. 

# Requirements
* 那种类型的数据分析？ 实时的，还是离线的？
* 是OLAP？

# 什么是OLAP
* 一个轻量级的基于Python的OLAP系统: https://github.com/DataBrewery/cubes

# 选型
* Kylin: 美团对大数据量OLAP的点评： https://zhuanlan.zhihu.com/p/27461561

# Legacy data system
* Oracle
* MySQL
* MongoDB
* Access

# Question
* Incremental copy data from RDBMS to HDFS?
* Sqoop support converters?

# Ideas
* Use VIEW definition to fill the gap.

# MongoDB to Hadoop
* https://docs.mongodb.com/ecosystem/tools/hadoop/

# Others
* 数据量大，数据是分布式存储的，数据分析的逻辑也是在分布式计算框架上执行的。
* 数据分析的接口。Apache Kylin提供了SQL, RESTful API. 有了SQL, 就可以在Excel, PowerBI, Tableau使用这些可视化地查看，探索这些数据。

# 相关产品或开源软件
* MyCat. http://mycat.io/. 基于MySQL做数据库集群，本质是个数据库中间件。

# Load RDBMS Data to/from HDFS
* https://coderwall.com/p/kgrwwq/sqoop-data-transfer-tool-from-rdbms-to-hadoop-box

# Reference
* Apache Kylin: https://share.iclient.ifeng.com/news/shareNews?forward=1&aid=109568477&aman=&gud=#backhead

* PB-Level data analysis:   http://e.huawei.com/us/products/cloud-computing-dc/cloud-computing/bigdata/fusioninsight-libra

* Legacy Database: http://agiledata.org/essays/legacyDatabases.html
* Diff between Sqoop&Flume (Coupons use sqoop.)https://www.dezyre.com/article/sqoop-vs-flume-battle-of-the-hadoop-etl-tools-/176
* The tool of data ingestion to Hadoop: https://www.predictiveanalyticstoday.com/data-ingestion-tools/
* Demo很酷 Oralce到Hadoop: http://discover.attunity.com/replicate-express-registration.html
* Attunity as the Hadoop data ingestion tool: https://www.attunity.com/hadoop-data-ingestion-tool/ 

