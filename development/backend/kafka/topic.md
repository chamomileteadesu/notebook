# Topic

```sh
# list topic
./kafka-topics.sh --bootstrap-server localhost:9092 --list
# describe topic
./kafka-topics.sh --bootstrap-server localhost:9092 --describe
# create a topic
./kafka-topics.sh --bootstrap-server localhost:9092 --create --topic my_topic
# delete a topic
./kafka-topics.sh --bootstrap-server localhost:9092 --delete --topic my_topic
```
