prerequisites 
Java Development Kit (JDK)
Version: 11 or higher
Verify installation:
java -version
The output should show java 11 or later.
Apache Kafka

Version: Compatible with the Kafka Java client library used in the project.
Kafka Official Download


cd KafkaMessageProject
2. Install Apache Kafka
Option 1: Install Kafka Locally
Download Kafka from the official site: Kafka Downloads.
Extract the archive and navigate to the Kafka directory.
Start Zookeeper:
bash
Copy code
bin/zookeeper-server-start.sh config/zookeeper.properties
Start Kafka broker:
bash
Copy code
bin/kafka-server-start.sh config/server.properties


Option 2: Run Kafka Using Docker
Use the following docker-compose.yml file to run Kafka and Zookeeper:

yaml
Copy code
version: '3'
services:
  zookeeper:
    image: wurstmeister/zookeeper:3.4.6
    ports:
      - "2181:2181"
  kafka:
    image: wurstmeister/kafka:latest
    environment:
      KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181
      KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://localhost:9092
      KAFKA_LISTENERS: PLAINTEXT://:9092
    ports:
      - "9092:9092"
Run the services with:


4. Running the Applications
Kafka Producer
To run the producer application:

bash
Copy code
java -cp target/KafkaMessageProject.jar kafka.producer.KafkaProducerApp
Kafka Consumer
To run the consumer application:

bash
Copy code
java -cp target/KafkaMessageProject.jar kafka.consumer.KafkaConsumerApp
Replace target/KafkaMessageProject.jar with the actual path to the generated JAR file.

5. Running Tests
To run the unit tests:

Using Maven:
bash
Copy code
mvn test
Using Gradle:
bash
Copy code
./gradlew test


How the Project Works
KafkaProducerApp sends messages to a Kafka topic.
KafkaConsumerApp listens to the topic and processes incoming messages.
Tests for the producer and consumer validate the core functionality.
Troubleshooting
Kafka is not running

Ensure Kafka and Zookeeper services are running.
Class not found error

Verify that the correct JAR file is being referenced in the java -cp command.
Producer or Consumer is not working

Ensure the topic exists or enable topic auto-creation in Kafka.
Check the Kafka broker address and topic name configuration.
Contributing
Feel free to fork the repository, make improvements, and create pull requests. Contributions are welcome!

