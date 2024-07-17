# kafka_on_azure
Setup Kafka single cluster on azure with kraft mode

[Instruction Video](https://drive.google.com/drive/folders/1l7-kqUQEM-sglwhCWtmxYzX36i9w6COY?usp=sharing)

# CMD:

sudo apt install openjdk-11-jdk
--
wget https://downloads.apache.org/kafka/3.7.0/kafka_2.13-3.7.0.tgz
--
tar -xzf kafka_2.13-3.7.0.tgz
--
sudo mv kafka_2.13-3.7.0 /usr/local/kafka

--Server.properties
sudo nano /usr/local/kafka/config/kraft/server.properties

--UUID
/usr/local/kafka/bin/kafka-storage.sh format -t `/usr/local/kafka/bin/kafka-storage.sh random-uuid` -c /usr/local/kafka/config/kraft/server.properties
--

Start Zookeeper:
/usr/local/kafka/bin/zookeeper-server-start.sh /usr/local/kafka/config/zookeeper.properties

Start Kafka:
/usr/local/kafka/bin/kafka-server-start.sh /usr/local/kafka/config/kraft/server.properties

/usr/local/kafka/bin/kafka-server-start.sh -daemon /usr/local/kafka/config/kraft/server.properties

Sample:
sudo /usr/local/kafka/bin/kafka-topics.sh --bootstrap-server 20.189.123.132:9092,20.189.113.187:9092,20.189.73.98:9092 --version

sudo /usr/local/kafka/bin/kafka-topics.sh --bootstrap-server 20.189.123.132:9092,20.189.113.187:9092,20.189.73.98:9092 --list

sudo /usr/local/kafka/bin/kafka-topics.sh --create --bootstrap-server 20.189.123.132:9092,20.189.113.187:9092,20.189.73.98:9092 --topic multiBroker

sudo /usr/local/kafka/bin/kafka-console-producer.sh --bootstrap-server 20.189.123.132:9092,20.189.113.187:9092,20.189.73.98:9092 --producer.config /usr/local/kafka/config/producer.properties --topic multiBroker

sudo /usr/local/kafka/bin/kafka-console-consumer.sh --bootstrap-server 20.189.123.132:9092 --consumer.config /usr/local/kafka/config/consumer.properties --topic multiBroker --from-beginning

--
sudo /usr/local/kafka/bin/kafka-topics.sh --bootstrap-server 20.189.123.132:9092,20.189.113.187:9092,20.189.73.98:9092 --delete --topic multiBroker
