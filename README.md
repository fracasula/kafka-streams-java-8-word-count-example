In every shell:

```bash
export CONFLUENT_VERSION=latest
export DOCKER_MACHINE_IP=localhost
```

Shell 1:

```bash
docker-compose exec confluent-kafka-1 kafka-console-consumer \
    --bootstrap-server localhost:29092 \
    --topic word-count-input --from-beginning \
    --property value.deserializer=org.apache.kafka.common.serialization.StringDeserializer
```

Shell 2:

```bash
docker-compose exec confluent-kafka-1 kafka-console-consumer \
    --bootstrap-server localhost:29092 \
    --topic word-count-output --from-beginning \
    --property print.key=true \
    --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer \
    --property value.deserializer=org.apache.kafka.common.serialization.LongDeserializer
```

Shell 3:

```bash
docker-compose exec confluent-kafka-1 kafka-console-producer \
    --broker-list localhost:29092 \
    --topic word-count-input
```
