# Installation Steps

## Step 1 - Verifying Java Installation

Hopefully you have already installed java on your machine right now, so you just verify it using the following command.
```bash
$ java -version
```
If java is successfully installed on your machine, you could see the version of the installed Java.

### Step 1.1 - Download JDK
If Java is not downloaded, please download the latest version of JDK by visiting the following link and download latest version.
http://www.oracle.com/technetwork/java/javase/downloads/index.html
Now the latest version is JDK 8u 60 and the file is “jdk-8u60-linux-x64.tar.gz”. Please download the file on your machine.

### Step 1.2 - Extract Files
Generally, files being downloaded are stored in the downloads folder, verify it and extract the tar setup using the following commands.

```bash
$ cd /go/to/download/path
$ tar -zxf jdk-8u60-linux-x64.gz
```

### Step 1.3 - Move to Opt Directory
To make java available to all users, move the extracted java content to usr/local/java/ folder.

```bash
$ su
password: (type password of root user)
$ mkdir /opt/jdk
$ mv jdk-1.8.0_60 /opt/jdk/
```

### Step 1.4 - Set path
To set path and JAVA_HOME variables, add the following commands to ~/.bashrc file.
```bash
export JAVA_HOME =/usr/jdk/jdk-1.8.0_60
export PATH=$PATH:$JAVA_HOME/bin
```

Now apply all the changes into current running system.
```bash
$ source ~/.bashrc
```

### Step 1.5 - Java Alternatives
Use the following command to change Java Alternatives.
```bash
update-alternatives --install /usr/bin/java java /opt/jdk/jdk1.8.0_60/bin/java 100
```

### Step 1.6 − Now verify java using verification command (java -version) explained in Step 1.

## Step 2 - ZooKeeper Framework Installation
### Step 2.1 - Download ZooKeeper
To install ZooKeeper framework on your machine, visit the following link and download the latest version of ZooKeeper.
http://zookeeper.apache.org/releases.html
As of now, latest version of ZooKeeper is 3.4.12 (ZooKeeper-3.4.12.tar.gz).

### Step 2.2 - Extract tar file
Extract tar file using the following command
```bash
$ cd opt/
$ tar -zxf zookeeper-3.4.12.tar.gz
$ sudo ln -s /opt/zookeeper-3.4.12 /opt/zookeeper
$ cd zookeeper
$ mkdir data
```

### Step 2.3 - Create Configuration File
Open Configuration File named conf/zoo.cfg using the command vi “conf/zoo.cfg” and all the following parameters to set as starting point.
```bash
$ vi conf/zoo.cfg
tickTime=2000
dataDir=/path/to/zookeeper/data
clientPort=2181
initLimit=5
syncLimit=2
```

Once the configuration file has been saved successfully and return to terminal again, you can start the zookeeper server.

### Step 2.4 - Start ZooKeeper Server
```bash
$ bin/zkServer.sh start
```

After executing this command, you will get a response as shown below −

```bash
$ JMX enabled by default
$ Using config: /Users/../zookeeper/bin/../conf/zoo.cfg
$ Starting zookeeper ... STARTED
```

### Step 2.5 - Start CLI

```bash
$ bin/zkCli.sh
```

After typing the above command, you will be connected to the zookeeper server and will get the below response.

```bash
Connecting to localhost:2181
................
................
................
Welcome to ZooKeeper!
................
................
WATCHER::
WatchedEvent state:SyncConnected type: None path:null
[zk: localhost:2181(CONNECTED) 0]
```

### Step 2.6 - Stop Zookeeper Server
After connecting the server and performing all the operations, you can stop the zookeeper server with the following command

```bash
$ bin/zkServer.sh stop
```

Now you have successfully installed Java and ZooKeeper on your machine. Let us see the steps to install Apache Kafka.

## Step 3 - Apache Kafka Installation

Let us continue with the following steps to install Kafka on your machine.

### Step 3.1 - Download Kafka
To install Kafka on your machine, click on the below link −
https://www-us.apache.org/dist/kafka/2.1.0/kafka_2.12-2.1.0.tgz
Now the latest version i.e., – kafka_2.12-2.1.0.tgz will be downloaded onto your machine.

### Step 3.2 - Extract the tar file
Extract the tar file using the following command −
```bash
$ cd opt/
$ tar -zxf kafka_2.12-2.1.0.tgz
$ sudo ln -s /opt/kafka_2.12-2.1.0 /opt/kafka
$ cd kafka
```

Now you have downloaded the latest version of Kafka on your machine.

### Step 3.3 - Start Server
You can start the server by giving the following command −
```bash
$ bin/kafka-server-start.sh config/server.properties
```

After the server starts, you would see the below response on your screen −

```bash
$ bin/kafka-server-start.sh config/server.properties
[2016-01-02 15:37:30,410] INFO KafkaConfig values:
request.timeout.ms = 30000
log.roll.hours = 168
inter.broker.protocol.version = 0.9.0.X
log.preallocate = false
security.inter.broker.protocol = PLAINTEXT
…………………………………………….
…………………………………………….
```

## Step 4 - Stop the Server
After performing all the operations, you can stop the server using the following command −
```bash
$ bin/kafka-server-stop.sh config/server.properties
```
Now that we have already discussed the Kafka installation, we can learn how to perform basic operations on Kafka in the next chapter.


# Apache Kafka - Basic Operation

### Modify .bash_profile or .profile
```bash
export KAFKA_HOME=/opt/kafka
```

### Start Zookeeper
```bash
sudo $KAFKA_HOME/bin/zookeeper-server-start.sh -daemon $KAFKA_HOME/config/zookeeper.properties
```
### Start Kafka Broker

```bash
sudo $KAFKA_HOME/bin/kafka-server-start.sh -daemon $KAFKA_HOME/config/server.properties
```

# Single Node-Single Broker Configuration
In this configuration you have a single ZooKeeper and broker id instance. Following are the steps to configure it −

### Creating a Kafka Topic
Kafka provides a command line utility named kafka-topics.sh to create topics on the server. Open new terminal and type the below example.

**Syntax**
```bash
sudo $KAFKA_HOME/bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic topic-name
```
**Example**
```bash
sudo $KAFKA_HOME/bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic stock-quote
```

We just created a topic named stock-quote with a single partition and one replica factor. The above created output will be similar to the following output −
```bash
Output − Created topic stock-quote
```

Once the topic has been created, you can get the notification in Kafka broker terminal window and the log for the created topic specified in “/tmp/kafka-logs/“ in the config/server.properties file.

### List of Topics
To get a list of topics in Kafka server, you can use the following command −

**Syntax**
```bash
sudo $KAFKA_HOME/bin/kafka-topics.sh --list --zookeeper localhost:2181
```

**Output**
```bash
stock-quote
```

Since we have created a topic, it will list out stock-quote only. Suppose, if you create more than one topics, you will get the topic names in the output.

### Start Producer to Send Messages
**Syntax**
```bash
sudo $KAFKA_HOME/bin/kafka-console-producer.sh --broker-list localhost:9092 —topic topic-name
```

From the above syntax, two main parameters are required for the producer command line client −

**Broker-list** − The list of brokers that we want to send the messages to. In this case we only have one broker. The Config/server.properties file contains broker port id, since we know our broker is listening on port 9092, so you can specify it directly.
**Topic name** − Here is an example for the topic name.

**Example**
```bash
sudo $KAFKA_HOME/bin/kafka-console-producer.sh --broker-list localhost:9092 --topic Hello-Kafka
```

The producer will wait on input from stdin and publishes to the Kafka cluster. By default, every new line is published as a new message then the default producer properties are specified in config/producer.properties file. Now you can type a few lines of messages in the terminal as shown below.

**Output**
```bash
$ sudo $KAFKA_HOME/bin/kafka-console-producer.sh --broker-list localhost:9092 --topic Hello-Kafka
[2016-01-16 13:50:45,931] WARN property topic is not valid (kafka.utils.Verifia-bleProperties)
Hello
My first message
My second message
```

### Start Consumer to Receive Messages
Similar to producer, the default consumer properties are specified in config/consumer.properties file. Open a new terminal and type the below syntax for consuming messages.

**Syntax**
```bash
sudo $KAFKA_HOME/bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic topic-name --from-beginning
```

**Example**
```bash
sudo $KAFKA_HOME/bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic stock-quote --from-beginning
Output
Hello
My first message
My second message
```

Finally, you are able to enter messages from the producer’s terminal and see them appearing in the consumer’s terminal. As of now, you have a very good understanding on the single node cluster with a single broker. Let us now move on to the multiple brokers configuration.
