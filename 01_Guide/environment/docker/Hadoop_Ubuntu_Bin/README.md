# Create Image

```bash
$ ./build-image.sh base-dnsmasq
$ ./build-image.sh hadoop-base
$ ./build-image.sh hbase-base
```

# Start Container

```bash
$ cd ~
$ ./start-hadoop-container.sh latest 3
# start master container...
# start slave1 container...
# start slave2 container...
```

# Serf agent

```bash
$ serf members

# master.trex.com  172.17.0.2:7946  alive  
# slave1.trex.com  172.17.0.3:7946  alive
# slave2.trex.com  172.17.0.4:7946  alive

$ cd ~
$ ./configure-members.sh
```

# Start Hadoop

```bash
$ ./start-hadoop.sh

$ jps
$HADOOP_HOME/bin/hdfs dfsadmin -report
```

# WordCount-1

### upload file

```bash
$HADOOP_HOME/bin/hadoop fs -mkdir /input
$HADOOP_HOME/bin/hadoop fs -ls /
$HADOOP_HOME/bin/hadoop fs -put $HADOOP_HOME/LICENSE.txt /input
$HADOOP_HOME/bin/hadoop fs -put $HADOOP_HOME/NOTICE.txt /input
$HADOOP_HOME/bin/hadoop fs -put $HADOOP_HOME/README.txt /input
$HADOOP_HOME/bin/hadoop fs -ls /input

```

### run jar
```bash
$HADOOP_HOME/bin/hadoop jar $HADOOP_HOME/share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.3.jar wordcount /input /output
```

### check result

```bash
$HADOOP_HOME/bin/hadoop fs -ls /output
$HADOOP_HOME/bin/hadoop fs -cat /output/part-r-00000
```

# WordCount-2

### upload file

```bash
$HADOOP_HOME/bin/hadoop fs -mkdir /user
# /user/<username>
$HADOOP_HOME/bin/hadoop fs -mkdir /user/root
$HADOOP_HOME/bin/hadoop fs -mkdir /user/root/input
$HADOOP_HOME/bin/hadoop fs -ls /
$HADOOP_HOME/bin/hadoop fs -put $HADOOP_HOME/LICENSE.txt /user/root/input
$HADOOP_HOME/bin/hadoop fs -put $HADOOP_HOME/NOTICE.txt /user/root/input
$HADOOP_HOME/bin/hadoop fs -put $HADOOP_HOME/README.txt /user/root/input
$HADOOP_HOME/bin/hadoop fs -ls /user/root/input
```

### run jar

```bash
$HADOOP_HOME/bin/hadoop jar $HADOOP_HOME/share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.3.jar wordcount /user/root/input /user/root/output
```

### check result

```bash
$HADOOP_HOME/bin/hadoop fs -ls /user/root/output
$HADOOP_HOME/bin/hadoop fs -cat /user/root/output/part-r-00000
```


