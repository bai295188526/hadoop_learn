# hadoop_learn
hadoop学习,hdfs,MapReduce实现单词统计

https://pan.baidu.com/s/1i4DR9ml

链接：https://pan.baidu.com/s/1qY40iYS 密码：wmx2

链接：https://pan.baidu.com/s/1pLgfAOF 密码：wion


## hadoop组成
+ HDFS : 分布式文件系统,存储海量的数据
    + namenode 管理节点,存放文件元数据(文件与数据库的映射表,数据块与数据节点映射表)
    + datanode 存放数据块
+ MapReduce : 并行处理框架,实现任务分解和调度

## hadoop应用
+ 搭建大型数据仓库,PB级数据的存储、处理、分析、统计等业务

## hadoop安装
+ linux环境
+ 安装jdk
+ 配置hadoop
    + **下载hadoop** 
    ```  
    wget https://archive.apache.org/dist/hadoop/common/hadoop-1.2.1/hadoop-1.2.1.tar.gz
    ```
    + **修改conf/hadoop-env.sh(修改JAVA_HOME为自己的java安装目录)** 
    ```
      export JAVA_HOME=/home/software/java/jdk1.8.0_121/
    ```
    + **修改core-site.xml**
    ```xml
    <property>
     <name>hadoop.tmp.dir</name>
     <value>/hadoop</value>
    </property>
    <property>
     <name>dfs.name.dir</name>
     <value>/hadoop/name</value>
    </property>
    <property>
     <name>fs.default.name</name>
     <value>hdfs://localhost:9000</value>
    </property>
    ```
    + **修改hdfs-site.xml**
    ```xml
    <property>
     <name>dfs.data.dir</name>
     <value>/hadoop/data</value>
    </property>
    ```
    + **修改mapred-site.xml**
    ```xml
    <property>
     <name>mapred.job.tracker</name>
     <value>localhost:9001</value>
    </property>
    ```
    + **修改/etc/profile 添加HADOOP_HOME**
    ```
    export HADOOP_HOME = /home/hadoop/hadoop-1.2.1
    ```
    + **修改/etc/profile 修改path**
    ```
    export PATH=$JAVA_HOME/bin:$JAVA_HOME/jre/bin:$HADOOP_HOME/bin:$PATH
    ```
    + **使修改生效**
    ```
    source /etc/profile
    ```
    + **执行hadoop命令成功则说明hadoop安装成功了**

+ **hadoop启动**
    + **格式化namenode**
    ```
    hadoop nodename -format
    ```
    + 启动服务
    ```
    hadoop/bin/start-all.sh
    ```
    
    
## hdfs基本命令
+ hadoop fs -put file(文件路径) path(hdfs路径) 将本地文件上传到hdfs
+ hadoop fs -mkdir 在hdfs创建路径
+ hadoop fs -get file(文件在hdfs的路径) path(本地路径)
+ hadoop dfsadmin -report (显示hdfs的信息,存储量等)

## MapReduce
### MapReduce基本原理
+ 分而治之,一个大任务分成多个小任务(Map),并行执行后,合并结果(reduce)

## hadoop经典例子
#### 单次计数
**统计单词出现的频率,结果按照字母表顺序排列**
+ 源代码地址[http://git.xiaopangad.cn/git/git/baijw/wordcount.git](http://note.youdao.com/)
+ 执行jps查看hadoop是否正常运行(可不执行)
+ 在hdfs创建输入
```
hadoop fs -mkdir input
```
+ 创建输入文件file1,file2(单词组合)
+ 把输入文件上传到hdfs
```
hadoop fs -put file(输入) input
```
+ 执行程序(打成jar包)
```
 hadoop jar WordCount.jar cn.baijw.code.hadoop_learn.WordCount input result
```

