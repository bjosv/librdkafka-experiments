# librdkafka-experiments

## Build librdkafka
```
 ./configure
make

# Run test
cd tests
> Run all in parallel
./interactive_broker_version.py 3.4.0
make

> Run single test
./interactive_broker_version.py 3.4.0
TESTS=0061 make

> Run single test with logs
./interactive_broker_version.py 3.4.0
TESTS=0061 TEST_DEBUG=cgrp,fetch make

./interactive_broker_version.py 3.4.0
TESTS=0031 TEST_DEBUG=mock make

> Run single test that only works in a scenario (see test.c and the .scenario for _TEST)
./interactive_broker_version.py 3.4.0 --scenario noautocreate
TESTS=0107 TEST_DEBUG=topic,metadata make

# Clean
make distclean
make clean
```

## Start cluster and enter a shell
python3 -m trivup.clusters.KafkaCluster --version 3.4.0

> bootstrap.servers PLAINTEXT://localhost:57897,PLAINTEXT://localhost:45025,PLAINTEXT://localhost:52037

### Check cluster
```
<librdkafka>/examples/describe_cluster -b PLAINTEXT://localhost:57897,PLAINTEXT://localhost:45025,PLAINTEXT://localhost:52037 1
<librdkafka>/examples/producer PLAINTEXT://localhost:57897,PLAINTEXT://localhost:45025,PLAINTEXT://localhost:52037 my-topic
<librdkafka>/examples/describe_topics -b PLAINTEXT://localhost:57897,PLAINTEXT://localhost:45025,PLAINTEXT://localhost:52037 1 my-topic
<librdkafka>/examples/list_offsets -b PLAINTEXT://localhost:57897,PLAINTEXT://localhost:45025,PLAINTEXT://localhost:52037 1 my-topic 0 0

```
