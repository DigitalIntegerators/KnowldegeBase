# install kafka on windows

## first install java 

https://www.oracle.com/eg/java/technologies/downloads/#jdk20-windows

to assert java installion run 

``` java --version ```

## second install kafka

## download kafka : [Binary downloads] version

https://kafka.apache.org/downloads

extract the pakage to the windows partion and rename it to kafka

c:\kafka

## edit config files 

open config\server.properties file 

serch for :``` log.dirs=/tmp/kafka-logs ```

edit it to : ``` log.dirs=c:/kafka/kafka-logs ``` 

save and exit 

open config\zookeeper file

serch for :``` dataDir=/tmp/zookeeper ```

edit it to :``` dataDir=c:/kafka/zookeeper-data ```

open cmd from kafka directory 

first start zookeeper with command

``` .\bin\windows\zookeeper-server-start.bat .\config\zookeeper.properties ```

then start kafka server with command

``` .\bin\windows\kafka-server-start.bat config\server.properties ```

to create topic 

``` .\bin\windowskafka-topics.bat --create --bootstrap-server localhost:9092 --topic <topicname> ```

to listen on the topic 

``` .\bin\windows\kafka-console-consumer.bat --topic <topicname> --bootstrap-server localhost:9092 --from-beginning ```

to push on to the topic from terminal to topic on the port

``` .\bin\windows\kafka-console-producer.bat --brocker-list localhost:9092 --topic <topicname> ```

https://github.com/open-telemetry/opentelemetry-collector-contrib/tree/main/exporter/kafkaexporter



















