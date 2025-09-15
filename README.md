🚀 Kafka 3.9.1 + Spring Boot Setup Guide
1️⃣ Download and Extract Kafka
Download Kafka 3.9.1 (Scala 2.13): kafka_2.13-3.9.1.tgz (asc, sha512)
Extract the file to a custom path, e.g., C:\kafka_3.9.1
Navigate to the extracted folder:
cd kafka_2.13-3.9.1


2️⃣ Environment Setup
Java JDK: Install Java 8 or higher.
Set JAVA_HOME:
JAVA_HOME=C:\Program Files\Java\jdk-<version>
PATH=%JAVA_HOME%\bin;%PATH%
Update PATH: Add Kafka bin\windows directory to PATH for easy command access.

3️⃣ Configure Zookeeper
Edit config/zookeeper.properties:
dataDir=C:/kafka_3.9.1/temp/zookeeper
clientPort=2181

4️⃣ Configure Kafka Broker
Edit config/server.properties:
broker.id=0
log.dirs=C:/kafka_3.9.1/temp/kafka-logs
zookeeper.connect=localhost:2181
listeners=PLAINTEXT://localhost:9092
num.partitions=1
auto.create.topics.enable=true

5️⃣ Start Zookeeper
.\bin\windows\zookeeper-server-start.bat .\config\zookeeper.properties

6️⃣ Start Kafka Broker
.\bin\windows\kafka-server-start.bat .\config\server.properties

7️⃣ Create a Topic
.\bin\windows\kafka-topics.bat --create --topic CodeDecodeTopic --bootstrap-server localhost:9092 --partitions 1 --replication-factor 
List topics:
.\bin\windows\kafka-topics.bat --list --bootstrap-server localhost:9092

8️⃣ Test Kafka in CMD
Producer:
Run this command another cmd
.\bin\windows\kafka-console-producer.bat --topic CodeDecodeTopic --bootstrap-server localhost:9092

Type your message (e.g., HelloKafka) → press Enter
Consumer:
.\bin\windows\kafka-console-consumer.bat --topic CodeDecodeTopic --from-beginning --bootstrap-server localhost:9092
You will see HelloKafka printed


🔟 Test With Spring Boot
Run Spring Boot app:
mvn spring-boot:run
Open browser or Postman:
GET http://localhost:8080/rest/api/producer?message=HelloKafka
