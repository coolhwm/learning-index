# Hadoop 大数据平台 - 学习笔记
## 1. 简介

### 1.1 时代背景
- 数据量、数据增长数据越来越快；
- 通过挖掘数据获得价值；
- 随着数据量越来越大，数据分析可能遇到各种瓶颈；

### 1.2  大数据关键技术
- MapReduce
- BigTable
- GFS

### 1.3 革命性变化
- 降低成本、使用PC及代替大型机、高端存储；
- 软件容错硬件故障视为常态，通过软件保证可靠性；
- 简化并行分布式计算，无需控制节点同步；

### 1.4 Hadoop
- 属于Apache旗下的开源软件；
- 是一个分部署存储及分布式计算平台；

#### 1.4.1 核心组成
- HDFS ：分布式文件系统，存储海量的数据；
- MapReduce：并行处理框架，实现任务分解和调度；

#### 1.4.2 作用
- 搭建大型数据仓库、PB级数据存储、分析、处理、统计；
- 搜索引擎、商业智能、日志分析、数据挖掘；

#### 1.4.3 优势
- 高扩展：可以方便的扩展硬件增加处理能力；
- 低成本：基于廉价硬件堆叠系统、通过软件容错实现系统可靠性；
- 成熟的生态圈：有很多周边工具、技术栈完整；

#### 1.4.4 应用情况
- 国内外IT公司均利用官方；
- 业界大数据平台的首选方案；
- 人才需求广泛（开发/运维）；

#### 1.4.5 生态系统
- MapReduce/HDFS
- HIVE ： 不用编写任务，直接编写SQL语句、降低Hadoop的门槛；
- HBASE：存储结构化数据的分布式数据库，放弃了事务特性、追求更高的扩展；
- Zookeeper：监控Hadoop集群状态、维护节点之间的数据一致性；

#### 1.4.6 版本
- 1.X 
- 2.X 

## 2. 安装Hadoop 

### 2.1 安装JDK 
在Ubuntu环境下安装JDK 1.7：
``` bash
# apt-get install openjdk-7-jdk
```

配置环境变量：


### 2.2 安装Hadoop
#### 2.2.1 下载
下载1.2.1版本的Hadoop：
```
wget https://archive.apache.org/dist/hadoop/common/hadoop-1.2.1/hadoop-1.2.1.tar.gz
```
各种版本可以在下载：[Hadoop发布版本下载地址](https://archive.apache.org/dist/hadoop/common/)

解压缩安装包：
```
tar -zxvf hadoop-1.2.1.tar.gz
```

#### 2.2.2 修改配置文件
配置`/conf/hadoop-evn.sh`：
``` bash
export JAVA_HOME=/root/data/jdk/jdk1.8.0_92
```

配置`/conf/core-site.xml`（Haddop核心配置）：
``` xml
<configuration>
	<!--Hadoop 的工作目录-->
	<property>
	    <name>hadoop.tmp.dir</name>
	    <value>/hadoop</value>
	</property>

	<!--namenode的元数据-->
	<property>
	    <name>dfs.name.dir</name>
	    <value>/hadoop/name</value>
	</property>

	<!--文件系统如何访问-->
	<property>
	    <name>fs.default.name</name>
	    <value>hdfs://127.0.0.1:9000</value>
	</property>

</configuration>
```

配置`/conf/hdfs-site.xml`（HDFS存储配置）：
``` xml
<configuration>
	<!--文件系统数据的目录-->
    <property>
        <name>dfs.data.dir</name>
        <value>/hadoop/data</value>
    </property>
<configuration>
```

配置`/conf/mapred-site.xml`（Map/Reduce配置）：
``` xml
<configuration>
	<!--任务调度器-->
    <property>
        <name>mapred.job.tracker</name>
        <value>http://127.0.0.1:9001</value>
    </property>
</configuration>
```

#### 2.2.3 修改环境变量
配置`/etc/profile`（环境变量）：
``` bash
#hadoop
HADOOP_HOME=/root/data/hadoop-1.2.1
PATH=$HADOOP_HOME/bin:$PATH
export HADOOP_HOME_WARN_SUPPRESS=1 # 防止出现警告
```

#### 2.2.4 初始化工作
格式化`namenode`：
``` bash
hadoop namenode -format
```
启动服务：
``` bash
sh start-all.sh
```

检查服务：
``` bash
jps
# 6496 Jps
# 6260 JobTracker
# 6421 TaskTracker
# 6181 SecondaryNameNode
# 5896 NameNode
# 6042 DataNode
```

检查存储：
``` bash
hadoop fs -ls /
# drwxr-xr-x   - root supergroup          0 2016-10-29 00:08 /hadoop
```
