# 1. Download Hadoop and Java

## [🔗 DOWNLOAD LINKs ](https://drive.google.com/drive/folders/1X75vXjnpuZOgTo9IqgqT2on-SwezgS71?usp=drive_link)

### `tar -zxvf hadoop-3.3.6.tar.gz`

### `tar -zxvf jdk-8u411-linux-x64.tar`

### `sudo nano ~/.bashrc`

```bash
**export JAVA_HOME=/home/<username>/BigData/jdk1.8.0_411
export HADOOP_HOME=/home/<username>/BigData/hadoop-3.3.6
export HIVE_HOME=/home/<username>/BigData/apache-hive-3.1.3-bin 
export SPARK_HOME=/home/<username>/BigData/spark-3.5.1-bin-hadoop3

export PATH=$JAVA_HOME/bin:$HADOOP_HOME/bin:$HADOOP_HOME/sbin/:$HIVE_HOME/bin:$SPARK_HOME/bin:$PATH
echo "Weclome, DATA ENGINEER!!"**
```

# 2. Modify Hadoop Configuration Files

> **NAMENODE ----> core-site.xml
RESOURCE MANGER ----> mapperd-site.xml
SECONDARYNAMENODE ---->
DATANODE ----> slaves
NODEMANGER ----> slaves & yarn-site.xml**
> 

### `sudo nano etc/hadoop/core-site.xml`

```bash
**<property>
<name>fs.default.name</name>
<value>hdfs://localhost:50000</value>
</property>**

```

### `sudo nano etc/hadoop/yarn-site.xml`

```bash
**<property>
<name>yarn.nodemanager.aux-services</name> <value>mapreduce_shuffle</value>
</property>
<property>
<name>yarn.nodemanager.aux-services.mapreduce.shuffle.class</name> <value>org.apache.hadoop.mapred.ShuffleHandler</value>
</property>
<property>
<description>The hostname of the RM.</description>
<name>yarn.resourcemanager.hostname</name>
<value>localhost</value>
</property>
<property>
<description>The address of the applications manager interface in the RM.</description>
<name>yarn.resourcemanager.address</name>
<value>localhost:8032</value>
</property>**
```

### `sudo nano etc/hadoop/hdfs-site.xml`

### change the "username" >> into user machine $USERNAME

```bash
**<property>
<name>dfs.namenode.name.dir</name>
<value>/home/<username>/hadoop2-dir/namenode-dir</value>
</property>
<property>
<name>dfs.datanode.data.dir</name>
<value>/home/<username>/hadoop2-dir/datanode-dir</value>
</property>**
```

### `sudo nano etc/hadoop/mapred-site.xml`

```bash
**<property>
<name>mapreduce.framework.name</name>
<value>yarn</value>
</property>
<property>
  <name>yarn.app.mapreduce.am.env</name>
  <value>HADOOP_MAPRED_HOME=/path/to/your/hadoop</value>
</property>
<property>
  <name>mapreduce.map.env</name>
  <value>HADOOP_MAPRED_HOME=/path/to/your/hadoop</value>
</property>
<property>
  <name>mapreduce.reduce.env</name>
  <value>HADOOP_MAPRED_HOME=/path/to/your/hadoop</value>
</property>**
```

### Add `JAVA_HOME` to all the bellow `*-env.sh` files:

### `vi etc/hadoop/hadoop-env.sh`
`export JAVA_HOME=/home/<username>/BigData/jdk1.8.0_411`

 `vi etc/hadoop/mapred-env.sh`
`export JAVA_HOME=/home/<username>/BigData/jdk1.8.0_411`

 `vi etc/hadoop/yarn-env.sh`
`export JAVA_HOME=/home/<username>/BigData/jdk1.8.0_411`

`vi etc/hadoop/slaves`
`localhost`

# Installing the SSH key

### (Generates, Manages and Converts Authentication keys)

```bash
**sudo apt-get install openssh-server
sudo ssh-keygen -t rsa
cd .ssh
ls
cat id_rsa.pub >> authorized_keys**
```

### (Setup passwordless ssh to localhost and to slaves )

### (Copy the id_rsa.pub from NameNode to authorized_keys in all machines)
 `ssh localhost`
(Asking No Password )

# 3. Format NameNode

```bash
**cd hadoop-3.3.6
bin/hadoop namenode -format (Your Hadoop File System Ready)**
```

# 4. Start All Hadoop Related Services

```bash
**sbin/start-all.sh**

```

### (Starting Daemon’s For DFS & YARN)

**NameNode
DataNode
SecondaryNameNode
ResourceManager
NodeManager**

# 5. check the Browser Web GUI

### NameNode - http://localhost:50070/
			 http://localhost:9870/

### Resource Manager - http://localhost:8088/

# 5.Stop All Hadoop and Yarn Related Services

```bash

 **sbin/stop-all.sh**
```
