# Hello Kafka with Confluent Platform for .NET

1. Start **Confluent Platform** using **Docker**
   - Instructions: https://docs.confluent.io/current/quickstart/ce-docker-quickstart.html
   - Clone **cp-all-in-one** repo
        ```
        git clone https://github.com/confluentinc/cp-all-in-one
        cd cp-all-in-one
        git checkout 5.5.0-post
        cd cp-all-in-one/
        ```
   - Start Confluent Platform
        ```
        docker-compose up -d --build
        docker-compose ps
        ```
   - Open Control Center web interface: http://localhost:9021/
     - Select your cluster
2. Create a topic in the Control Center
   - Go to Topics, click Add Topic
   - Enter topic name: testTopic1
   - Click Create with Defaults
3. Consume messages from a terminal
   - Open terminal and run:
        ```
        docker exec -it broker bash
        ```
   - Run the consumer console
        ```
        cd /usr/bin
        ./kafka-console-consumer --bootstrap-server broker:29092 --topic testTopic1
        ```
4. Produce messages from a terminal
   - Open terminal and run:
        ```
        docker exec -it broker bash
        ```
   - Run the consumer console
        ```
        cd /usr/bin
        ./kafka-console-producer --broker-list broker:29092 --topic testTopic1
        ```
   - Type a message and hit enter. Repeat seveeral times.
     - These will appear in the consumer terminal.
        ```
        >Hello
        >World
        Again
        ```
5. Create a **Consumer** client
   - Create .NET Core console app
        ```
        dotnet new console -n consumer
        cd consumer
        ```
   - Add **Confluent.Kafka** package
        ```
        dotnet add package Confluent.Kafka
        ```
   - Copy [program.cs](https://github.com/confluentinc/confluent-kafka-dotnet/blob/master/examples/Consumer/Program.cs) from consumer example in confluent-kafka-dotnet
   - Run the consumer to view messages for a topic.
        ```
        dotnet run manual localhost:9092 testTopic2
        ```
6. Create a **Producer** client
   - Confluent .NET Wiki: https://github.com/confluentinc/confluent-kafka-dotnet/wiki
   - Create .NET Core console app
        ```
        dotnet new console -n producer
        cd producer
        ```
   - Add **Confluent.Kafka** package
        ```
        dotnet add package Confluent.Kafka
        ```
   - Copy [program.cs](https://github.com/confluentinc/confluent-kafka-dotnet/blob/master/examples/Producer/Program.cs) from producer example in confluent-kafka-dotnet
   - Run the producer to create a topic and send messages.
        ```
        dotnet run localhost:9092 testTopic2
        ```
   - To see usage run: `dotnet run`
   - When prompted enter key value: `1 hello world`
     - Repeat several times
   - Press Ctrl+C to terminate
