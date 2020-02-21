---
title: Apache Kafka
definition: Distributed Streaming Platform
tags: event stream message broker queue publish subscribe zookeeper
---

- Messaging system (publish/subscribe pattern)
- Distributed storage (store data in a fault-tolerant, durable way)
- Data processing (process events as they occur)

## Event Driven Architecture (EDA)

### Examples

- Microservices
- Serverless
- FaaS
- Streaming
- Event Sourcing
- CQRS (Command Query Responsibility Segregation)

### Drawbacks

- Steep learning curve
- Complexity
- Loss of transactionality
- Lineage (tracking event through system)

### Event Storming

- Domain event
- Policy ("whenever this, do that")
- External system
- Command

Tool: Miro

### DDD

- Aggregate
- Bounded context (Order, Payment, Shipping)

## Kafka

### Why Kafka

- Open source
- Java (popular, lots of developers, debuging)
- High throughput (no serialization/deserialization, zero copy)
- More than a messaging system

### Components

- Broker (running application on OS/HW, which takes messages and stores them on
  HD or reads them from HD)
- Zookeeper (keeps list of brokers & configuration, checks broker availability)
- Cluster (multiple brokers, for scalability, fault-tolerance, high throughput)
- Record (key, value, timestamp)
- Topic (can be on multiple brokers, since kafka is distributed)
  - delete: remove msg if topic gets too big or no new msg received
  - compact: msg with same key gets replaced with existing one or added if key
    is new
- Partition (help splitting the load across brokers)
  - same topic gets split over multiple partitions where each partition is
    stored on different broker
  - if number of partition is bigger than number of brokers, multiple partition
    get stored on same broker :(
  - each partition will store different messages, i.e. same message will not
    exist in different partition
  - Partitions get replicated in order to keep fault-tolerance
- Producer
  - creates & transmits events to kafka
  - creates a record which it needs to serialize (key/value-serializer)
  - Serializer: Avro, Protobuf, Thrift, JSON, XML, YAML
- Consumer
  - uses pull to get new messages
  - multiple consumers can "act" as one if they are in the same consumer-group
- Schema registry (e.g. confluent)

### Streams

- topology
- source
- processor: stateless/stateful, sink, state store,
- duality: stream/table

### KSQL

- Abstraction over Kafka streams with a SQL syntax
- windowing: tumbling & hopping

### Kafka Connect

- Use case: store kafka message in DB/S3 bucket
- Standalone vs. distributed mode
