    
# Hadoop 大数据平台 - 学习笔记

## 1. 简介
> Apache Hadoop软件库是一个框架，允许在集群服务器上使用简单的编程模型对大数据集进行分布式处理。Hadoop被设计成能够从单台服务器扩展到数以千计的服务器，每台服务器都有本地的计算和存储资源。Hadoop的高可用性并不依赖硬件，其代码库自身就能在应用层侦测并处理硬件故障，因此能基于服务器集群提供高可用性的服务。
![生态系统](./1478283337935.png)
- `HDFS`：分布式文件系统，数据保存在计算机集群上，为HBase等工具提供了基础；
- `MapReduce`：分布式、并行处理编程模型，将任务分成map和reduce，能够实现快速访问数据；
- `HBase`：建立在HDFS上，面向列的NoSQL数据库，用于读/写大量数据。
- `Zookeeper`：分布式协调服务，运行在计算机集群上面，用于管理Hadoop操作；
- `Pig`：MapReduce编程的复杂性抽象，其编译期将`Pig Latin`脚本语言翻译成MR程序序列；
- `Hive`：类似SQL的高级语言，在Hadoop上查询语句；
- `Sqoop`：一种用于在关系数据库、数据仓库和Hadoop之间转移数据的连接工具；
- `Flume`：用于收集、汇总大数据、将大量数据转移到HDFS的服务；

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

## 3. HDFS 文件系统
> Hadoop分布式文件系统(`HDFS`，`Hadoop Distributed File System` )被设计成适合运行在通用硬件(commodity hardware)上的分布式文件系统。HDFS有着高容错性（fault-tolerant）的特点，并且设计用来部署在低廉的（low-cost）硬件上。
> 而且它提供高吞吐量（high throughput）来访问应用程序的数据，适合那些有着超大数据集（large data set）的应用程序。HDFS放宽了（relax）POSIX的要求（requirements）这样可以实现流的形式访问（streaming access）文件系统中的数据。

### 3.1 基本概念
- `Block` - HDFS的文件被分成块进行存储，每个块的大小默认为`64MB`，块是文件存储处理的逻辑单元；
- `NameNode` - 管理节点，存放文件元数据；包括文件和数据块的映射表、数据块和数据节点的映射表；
- `DataNode`- 工作节点，存放真正的数据块；

**HDFS体系结构图：**
![HDFS](./1477760831760.png)

**HDFS的特点：**
- 数据冗余、硬件容错；
- 流式数据访问（一次存储、多次读取）；
- 存储大文件；
- 适合批量读写、吞吐量高、一次接卸多次读取；
- 不适合交互式应用，低延迟很难满足；

### 3.2 数据管理与容错
- **数据块副本：**每个数据块3个副本，分布在两个机架内的三个节点；防止单节点故障和机架故障；
- **心跳检测：**`DataNode`定期向`NameNode`发送心跳消息，发送节点状态；
- **SecondaryNameNode：**二级NameNode定期同步元数据镜像文件和修改日志，NameNode故障时二级NameNode工作，保证高可用性；

### 3.3 文件读写
**文件读取流程：**
- 客户端先向`NameNode`发起文件读取请求（文件名/路径），`NameNode`查询元数据返回客户端（包含块及其DataNode位置）；
- 客户端找到`DataNode`，读取`Block`并组装成文件；

**文件写入流程：**
- 文件拆分成`Block`；
- 客户端通知`NameNode`，`NameNode`返回空闲的DataNods；
- 客户端对`Blocks`进行写入操作；
- 执行流水线复制更新`NameNode`的元数据；
- 循环写入剩余的`Blocks`；

### 3.4 基础使用
格式化：
``` bash
hadoop namenode -format
```

基本命令：
``` bash
# 打印文件
hadoop fs -ls [path]

# 建立目录
hadoop fs -mkdir [dir_name]

# 上传文件
hadoop fs -pu [filename]

# 查看文件
hadoop fs -cat [filename]

# 下载文件
hadoop fs -get [src_name] [dis_name]

# 文件系统使用报告
hadoop dfsadmin -report
```

## 4. MapReduce 并行计算框架

### 4.1 基本原理
> 分而治之原理，将一个大任务分解成多个小任务(Map)，并行执行后再合并结果(Reduce)；

![MR举例](./1477845188688.png)
- 切分任务；
- 分别统计；
- 组合规约；
- 汇总统计；
> 例如统计100G的日志文件中，出现次数最多的IP地址，可以分为以下步骤：
> - 日志文件按照时间区段进行分解到不同的任务节点上（Map）；
> - 任务节点分别统计各个IP地址出现的次数；
> - 任务节点将统计结果，根据一定规则汇总规约（Reduce）；
> - 最终产生排序结果；


### 4.2 运行流程

#### 4.2.1 组成部分
- `Job` - 整体的作业；
- `Task` - 任务，一个`Job`由多个`Task`组成；
	- `MapTask`
	- `ReduceTask`
- `JobTracker` - 管理节点，负责分解Map任务和Reduce任务；
- `TaskTracker` - 任务处理节点，负责处理任务；
	- `MapTaskTracker`
	- `ReduceTaskTracker`

####4.2.2 JobTracker
- 作业调度；
- 任务分配、监控任务执行进度；
- 监控TaskTracker的状态；

#### 4.2.3 TaskTracker
- 执行任务；
- 汇报任务状态；

#### 4.2.4 执行过程
![MR执行过程](./1477848141097.png)
- 任务提交到`JboTracker`；
- 数据分片；
- Map端分配Map任务，由`MapTaskTracker`处理；
- 产生中间结果KEY-VALUE对；
- Reduce端分配Reudce任务，由`ReduceTaskTracker`处理；
- 写回结果的HSFS；

### 4.3 容错机制
- 重复执行：重复执行过任务4次后放弃；
- 推测执行：某个节点计算速度异常时，另外找一个节点负责处理；

Hadoop 大数据平台 - 学习笔记

01. 写字台


Hadoop 大数据平台 - 学习笔记
1. 简介
1.1 时代背景
1.2 大数据关键技术
1.3 革命性变化
1.4 Hadoop
1.4.1 核心组成
1.4.2 作用
1.4.3 优势
1.4.4 应用情况
1.4.5 生态系统
1.4.6 版本
2. 安装Hadoop
2.1 安装JDK
2.2 安装Hadoop
2.2.1 下载
2.2.2 修改配置文件
2.2.3 修改环境变量
2.2.4 初始化工作
3. HDFS 文件系统
3.1 基本概念
3.2 数据管理与容错
3.3 文件读写
3.4 基础使用
4. MapReduce 并行计算框架
4.1 基本原理
4.2 运行流程
4.2.1 组成部分
4.2.2 JobTracker
4.2.3 TaskTracker
4.2.4 执行过程
4.3 容错机制
1. 简介

Apache Hadoop软件库是一个框架，允许在集群服务器上使用简单的编程模型对大数据集进行分布式处理。Hadoop被设计成能够从单台服务器扩展到数以千计的服务器，每台服务器都有本地的计算和存储资源。Hadoop的高可用性并不依赖硬件，其代码库自身就能在应用层侦测并处理硬件故障，因此能基于服务器集群提供高可用性的服务。
生态系统

HDFS：分布式文件系统，数据保存在计算机集群上，为HBase等工具提供了基础；
MapReduce：分布式、并行处理编程模型，将任务分成map和reduce，能够实现快速访问数据；
HBase：建立在HDFS上，面向列的NoSQL数据库，用于读/写大量数据。
Zookeeper：分布式协调服务，运行在计算机集群上面，用于管理Hadoop操作；
Pig：MapReduce编程的复杂性抽象，其编译期将Pig Latin脚本语言翻译成MR程序序列；
Hive：类似SQL的高级语言，在Hadoop上查询语句；
Sqoop：一种用于在关系数据库、数据仓库和Hadoop之间转移数据的连接工具；
Flume：用于收集、汇总大数据、将大量数据转移到HDFS的服务；
1.1 时代背景

数据量、数据增长数据越来越快；
通过挖掘数据获得价值；
随着数据量越来越大，数据分析可能遇到各种瓶颈；
1.2 大数据关键技术

MapReduce
BigTable
GFS
1.3 革命性变化

降低成本、使用PC及代替大型机、高端存储；
软件容错硬件故障视为常态，通过软件保证可靠性；
简化并行分布式计算，无需控制节点同步；
1.4 Hadoop

属于Apache旗下的开源软件；
是一个分部署存储及分布式计算平台；
1.4.1 核心组成

HDFS ：分布式文件系统，存储海量的数据；
MapReduce：并行处理框架，实现任务分解和调度；
1.4.2 作用

搭建大型数据仓库、PB级数据存储、分析、处理、统计；
搜索引擎、商业智能、日志分析、数据挖掘；
1.4.3 优势

高扩展：可以方便的扩展硬件增加处理能力；
低成本：基于廉价硬件堆叠系统、通过软件容错实现系统可靠性；
成熟的生态圈：有很多周边工具、技术栈完整；
1.4.4 应用情况

国内外IT公司均利用官方；
业界大数据平台的首选方案；
人才需求广泛（开发/运维）；
1.4.5 生态系统

MapReduce/HDFS
HIVE ： 不用编写任务，直接编写SQL语句、降低Hadoop的门槛；
HBASE：存储结构化数据的分布式数据库，放弃了事务特性、追求更高的扩展；
Zookeeper：监控Hadoop集群状态、维护节点之间的数据一致性；
1.4.6 版本

1.X
2.X
2. 安装Hadoop

2.1 安装JDK

在Ubuntu环境下安装JDK 1.7：

# apt-get install openjdk-7-jdk
配置环境变量：

2.2 安装Hadoop

2.2.1 下载

下载1.2.1版本的Hadoop：

wget https://archive.apache.org/dist/hadoop/common/hadoop-1.2.1/hadoop-1.2.1.tar.gz
各种版本可以在下载：Hadoop发布版本下载地址

解压缩安装包：

tar -zxvf hadoop-1.2.1.tar.gz
2.2.2 修改配置文件

配置/conf/hadoop-evn.sh：

export JAVA_HOME=/root/data/jdk/jdk1.8.0_92
配置/conf/core-site.xml（Haddop核心配置）：

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
配置/conf/hdfs-site.xml（HDFS存储配置）：

<configuration>
    <!--文件系统数据的目录-->
    <property>
        <name>dfs.data.dir</name>
        <value>/hadoop/data</value>
    </property>
<configuration>
配置/conf/mapred-site.xml（Map/Reduce配置）：

<configuration>
    <!--任务调度器-->
    <property>
        <name>mapred.job.tracker</name>
        <value>http://127.0.0.1:9001</value>
    </property>
</configuration>
2.2.3 修改环境变量

配置/etc/profile（环境变量）：

#hadoop
HADOOP_HOME=/root/data/hadoop-1.2.1
PATH=$HADOOP_HOME/bin:$PATH
export HADOOP_HOME_WARN_SUPPRESS=1 # 防止出现警告
2.2.4 初始化工作

格式化namenode：

hadoop namenode -format
启动服务：

sh start-all.sh
检查服务：

jps
# 6496 Jps
# 6260 JobTracker
# 6421 TaskTracker
# 6181 SecondaryNameNode
# 5896 NameNode
# 6042 DataNode
检查存储：

hadoop fs -ls /
# drwxr-xr-x   - root supergroup          0 2016-10-29 00:08 /hadoop
3. HDFS 文件系统

Hadoop分布式文件系统(HDFS，Hadoop Distributed File System )被设计成适合运行在通用硬件(commodity hardware)上的分布式文件系统。HDFS有着高容错性（fault-tolerant）的特点，并且设计用来部署在低廉的（low-cost）硬件上。 
而且它提供高吞吐量（high throughput）来访问应用程序的数据，适合那些有着超大数据集（large data set）的应用程序。HDFS放宽了（relax）POSIX的要求（requirements）这样可以实现流的形式访问（streaming access）文件系统中的数据。
3.1 基本概念

Block - HDFS的文件被分成块进行存储，每个块的大小默认为64MB，块是文件存储处理的逻辑单元；
NameNode - 管理节点，存放文件元数据；包括文件和数据块的映射表、数据块和数据节点的映射表；
DataNode- 工作节点，存放真正的数据块；
HDFS体系结构图：

HDFS

HDFS的特点：

数据冗余、硬件容错；
流式数据访问（一次存储、多次读取）；
存储大文件；
适合批量读写、吞吐量高、一次接卸多次读取；
不适合交互式应用，低延迟很难满足；
3.2 数据管理与容错

数据块副本：每个数据块3个副本，分布在两个机架内的三个节点；防止单节点故障和机架故障；
心跳检测：DataNode定期向NameNode发送心跳消息，发送节点状态；
SecondaryNameNode：二级NameNode定期同步元数据镜像文件和修改日志，NameNode故障时二级NameNode工作，保证高可用性；
3.3 文件读写

文件读取流程：

客户端先向NameNode发起文件读取请求（文件名/路径），NameNode查询元数据返回客户端（包含块及其DataNode位置）；
客户端找到DataNode，读取Block并组装成文件；
文件写入流程：

文件拆分成Block；
客户端通知NameNode，NameNode返回空闲的DataNods；
客户端对Blocks进行写入操作；
执行流水线复制更新NameNode的元数据；
循环写入剩余的Blocks；
3.4 基础使用

格式化：

hadoop namenode -format
基本命令：

# 打印文件
hadoop fs -ls [path]

# 建立目录
hadoop fs -mkdir [dir_name]

# 上传文件
hadoop fs -pu [filename]

# 查看文件
hadoop fs -cat [filename]

# 下载文件
hadoop fs -get [src_name] [dis_name]

# 文件系统使用报告
hadoop dfsadmin -report
4. MapReduce 并行计算框架

4.1 基本原理

分而治之原理，将一个大任务分解成多个小任务(Map)，并行执行后再合并结果(Reduce)；
MR举例

切分任务；
分别统计；
组合规约；
汇总统计； 
例如统计100G的日志文件中，出现次数最多的IP地址，可以分为以下步骤： 

日志文件按照时间区段进行分解到不同的任务节点上（Map）； 
任务节点分别统计各个IP地址出现的次数； 
任务节点将统计结果，根据一定规则汇总规约（Reduce）； 
最终产生排序结果；

4.2 运行流程

4.2.1 组成部分

Job - 整体的作业；
Task - 任务，一个Job由多个Task组成； 
MapTask
ReduceTask
JobTracker - 管理节点，负责分解Map任务和Reduce任务；
TaskTracker - 任务处理节点，负责处理任务； 
MapTaskTracker
ReduceTaskTracker
4.2.2 JobTracker

作业调度；
任务分配、监控任务执行进度；
监控TaskTracker的状态；
4.2.3 TaskTracker

执行任务；
汇报任务状态；
4.2.4 执行过程

MR执行过程

任务提交到JboTracker；
数据分片；
Map端分配Map任务，由MapTaskTracker处理；
产生中间结果KEY-VALUE对；
Reduce端分配Reudce任务，由ReduceTaskTracker处理；
写回结果的HSFS；
4.3 容错机制

重复执行：重复执行过任务4次后放弃；
推测执行：某个节点计算速度异常时，另外找一个节点负责处理；
     4629 
fsneak
 退出账号
当前文档
 恢复至上次同步状态
 删除文档
 导出...
 预览文档
 分享链接
系统
 设置
 下载桌面客户端
 下载离线Chrome App
 使用说明
 快捷帮助
 常见问题
 关于

搜索文件
01. 写字台 Hadoop 大数据平台 - 学习笔记
01. 写字台 JavaScript 面向对象 - 学习笔记
02. 计划 2016年工作/生活月度总结
01. 写字台 Lucene - 学习笔记
归档
 B1. 资源管理
 02. Java
 C1. IT网管
 01. Web
 B3. 监控管理
 04. Linux
 01. 写字台
 05. Other
 B4. 运维管理
 02. 计划
 B2. 综合门户
 08. Reading

