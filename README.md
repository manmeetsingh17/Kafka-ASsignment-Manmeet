# Kafka-ASsignment-Manmeet
Consumer Producer Message Kafka

To produce the message as an Object:
Add your message in the Producer Record
for (int i = 1; i <= 10; i++) {
                User user = new User(i,"Manmeet",22,"MCA");
                kafkaProducer.send(new ProducerRecord("mytopic", String.valueOf(user.getId()), user));
                System.out.println(user);
            }
            
            mytopic is the name of the topic and User is the object in user class.
            
            
Writing the data into a file while consuming it
            while (true) {
                FileWriter fileWriter = new FileWriter("user-json-data.txt", true);

                ConsumerRecords<String, User> consumerRecords = kafkaConsumer.poll(Duration.ofSeconds(1));

                for (ConsumerRecord<String, User> consumerRecord : consumerRecords) {
                    System.out.printf(
                            "Topic: %s, Partition: %d, Value: %s%n",
                            consumerRecord.topic(),
                            consumerRecord.partition(),
                            consumerRecord.value().toString());

                    fileWriter.write(consumerRecord.value().toString() + "\n");
                }
                fileWriter.flush();
                fileWriter.close();
            }


Then run the consumer.java file and you'll see the messages from beginning produced by Producer.

