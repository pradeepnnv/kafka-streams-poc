# kafka-streams-poc
Kafka Streams POC

Reference: https://kafka.apache.org/30/documentation/streams/tutorial

### Pre-req

#### Start ZK.
```shell
zookeeper-server-start.sh config/zookeeper.properties
```

#### Start Kafka broker.
```shell
kafka-server-start.sh config/server.properties
```

#### Validate Kafka broker.
```shell
kafka-topics.sh --bootstrap-server localhost:9092 --list
```

#### Create required topics.
```shell
kafka-topics.sh --bootstrap-server localhost:9092 --create --topic streams-plaintext-input --partitions 1 --replication-factor 1
kafka-topics.sh --bootstrap-server localhost:9092 --create --topic streams-pipe-output --partitions 1 --replication-factor  1 
```

#### Start Producer
```shell
kafka-console-producer.sh --bootstrap-server localhost:9092 --topic streams-plaintext-input
```

#### Start Consumer
```shell
kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic streams-pipe-output
```

### Start Kafka Streams

```shell
cd streams.examples
mvn clean package exec:java -Dexec.mainClass=org.pradeepnnv.kafkastreams.poc.Pipe
```

### Testing

Type some input in the window where kafka producer is running. 
Same output should be observed in the consumer window. 