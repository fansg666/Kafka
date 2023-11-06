# Kafka安装步骤

在学习kafka时我们一般都是要使用zookeeper,在我看了许多csdn水文,差点给我把ubuntu搞崩，最后，经过无数次的尝试，我总结出来以下的下载安装步骤。

##### 我们使用的是ubuntu系统

##### 1.首先配置zookkeeper

如果你想先配置Zookeeper，然后将Kafka安装在`/opt/module`目录下，可以按照以下步骤进行操作：

1. 下载和解压Zookeeper：
   前往Apache ZooKeeper官方网站（https://zookeeper.apache.org/releases.html）下载最新的稳定版本的ZooKeeper，如果你下载完。压缩包他一般默认在下载那个目录里面，如果你想要解压到`/opt/module`目录，用以下命令
   
   ```shell
   sudo tar xzf apache-zookeeper-{zookeeper-version}.tar.gz -C /opt/module
   sudo mv /opt/module/apache-zookeeper-{zookeeper-version} /opt/module/zookeeper
   请确保将`{zookeeper-version}`替换为ZooKeeper的版本号。例如，如果要安装ZooKeeper 3.7.0，命令应该是：
   sudo tar xzf apache-zookeeper-3.7.0.tar.gz -C /opt/module
   sudo mv /opt/module/apache-zookeeper-3.7.0 /opt/module/zookeeper
   ```
   
   
   
1. 或者在终端中，使用以下命令下载并解压ZooKeeper到`/opt/module`目录：
   
   ````shell
   wget https://downloads.apache.org/zookeeper/{zookeeper-version}/apache-zookeeper-{zookeeper-version}.tar.gz
   sudo tar xzf apache-zookeeper-{zookeeper-version}.tar.gz -C /opt/module
   sudo mv /opt/module/apache-zookeeper-{zookeeper-version} /opt/module/zookeeper
   ```
   
   请确保将`{zookeeper-version}`替换为ZooKeeper的版本号。例如，如果要安装ZooKeeper 3.7.0，命令应该是：
   ````shell
   wget https://downloads.apache.org/zookeeper/3.7.0/apache-zookeeper-3.7.0.tar.gz
   sudo tar xzf apache-zookeeper-3.7.0.tar.gz -C /opt/module
   sudo mv /opt/module/apache-zookeeper-3.7.0 /opt/module/zookeeper
   ```
   
2. 配置Zookeeper：
   在Zookeeper目录中，创建一个名为`data`的文件夹用于存储Zookeeper的数据：
   ````shell
   sudo mkdir -p /opt/module/zookeeper/data
   ```
   
   复制`zoo_sample.cfg`文件并重命名为`zoo.cfg`：
   ````shell
   sudo cp /opt/module/zookeeper/conf/zoo_sample.cfg /opt/module/zookeeper/conf/zoo.cfg
   ```
   
   编辑`zoo.cfg`文件：
   ````shell
   sudo nano /opt/module/zookeeper/conf/zoo.cfg
   ```
   
   修改以下属性的值：
   ````
   
   ```
   dataDir=/opt/module/zookeeper/data
   保存文件并退出编辑器。

3. 启动Zookeeper服务：
   在终端中，使用以下命令启动Zookeeper服务：
   ````shell
   /opt/module/zookeeper/bin/zkServer.sh start
   ```

![image-20231107042625013](C:\Users\86198\AppData\Roaming\Typora\typora-user-images\image-20231107042625013.png)

如果出现这个画面则说明你zookeeper启动成功。

注意启动kafka之前先启动zookeeper

##### 2.配置kafka



 前往Apache Kafka官方网站（https://kafka.apache.org/downloads）下载最新的稳定版本的Kafka。

 如果你是在网站下载，和上面zookeeper那个差不多

  在终端中，使用以下命令下载并解压Kafka到`/opt/module`目录：

   ````shell
   wget https://downloads.apache.org/kafka/{kafka-version}/kafka_{scala-version}-{kafka-version}.tgz
   sudo tar xzf kafka_{scala-version}-{kafka-version}.tgz -C /opt/module
   sudo mv /opt/module/kafka_{scala-version}-{kafka-version} /opt/module/kafka
   ```

   请确保将`{kafka-version}`替换为Kafka的版本号，`{scala-version}`替换为Scala的版本号。例如，如果要安装Kafka 2.8.0和Scala 2.13.x，命令应该是：
   ````shell
   wget https://downloads.apache.org/kafka/2.8.0/kafka_2.13-2.8.0.tgz
   sudo tar xzf kafka_2.13-2.8.0.tgz -C /opt/module
   sudo mv /opt/module/kafka_2.13-2.8.0 /opt/module/kafka
   ```

5. 配置Kafka：
   编辑Kafka的配置文件：
   ````shell
   sudo nano /opt/module/kafka/config/server.properties
   ```

   修改以下属性的值：
      zookeeper.connect=localhost:2181
   ````

   ```

   保存文件并退出编辑器。

6. 启动Kafka服务：
   在终端中，使用以下命令启动Kafka服务：
   ````shell
   /opt/module/kafka/bin/kafka-server-start.sh /opt/module/kafka/config/server.properties
   //当然这个启动是看你在哪个目录下启动，那个 /opt/module/kafka/bin/和/opt/module/kafka/config/不是写死的
   
   ```

 现在，你已经完成了Zookeeper和Kafka的配置和启动。

请注意，上述步骤中的路径和命令是假设你的目标安装路径是`/opt/module`。你可以根据自己的需求修改路径。

![image-20231107043227350](C:\Users\86198\AppData\Roaming\Typora\typora-user-images\image-20231107043227350.png)

##### 3.启动后查看这个文件有没有启动成功：

![image-20231107043342521](C:\Users\86198\AppData\Roaming\Typora\typora-user-images\image-20231107043342521.png)

如果出现这种就是成功

##### 4.创建一个Topic test

![image-20231107043425106](C:\Users\86198\AppData\Roaming\Typora\typora-user-images\image-20231107043425106.png)

用以下命令行就行

~~~shell
如果你正在使用较新的Kafka版本，请尝试使用以下命令来创建主题：
```shell
./kafka-topics.sh --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic test
```
~~~

~~~shell

如果你正在使用较新的Kafka版本，请尝试使用以下命令来列出主题：
```shell
./kafka-topics.sh --list --bootstrap-server localhost:9092
```
~~~

