# config

```shell
# config topic retention time
./kafka-configs.sh --bootstrap-server localhost:9092 \
--entity-type topics \
--entity-name my_topic \
--alter --add-config retention.ms=10000
```
