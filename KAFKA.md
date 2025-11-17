<div align="center">

# ⚡ Apache Kafka: The Complete Guide

### _Distributed Event Streaming Platform for Real-Time Data Pipelines_

[![Kafka Version](https://img.shields.io/badge/Kafka-4.0+-ff6600?style=for-the-badge&logo=apache-kafka&logoColor=white)](https://kafka.apache.org/)
[![License](https://img.shields.io/badge/License-Apache_2.0-blue?style=for-the-badge)](https://www.apache.org/licenses/LICENSE-2.0)
[![Stars](https://img.shields.io/github/stars/apache/kafka?style=for-the-badge)](https://github.com/apache/kafka)
[![Last Updated](https://img.shields.io/badge/Updated-2025-green?style=for-the-badge)](https://kafka.apache.org/)

<p align="center">
  <a href="#-what-is-kafka">What is Kafka?</a> •
  <a href="#-getting-started">Getting Started</a> •
  <a href="#-architecture">Architecture</a> •
  <a href="#-deployment">Deployment</a> •
  <a href="#-performance">Performance</a> •
  <a href="#-resources">Resources</a>
</p>

</div>

---

## 📋 Table of Contents

- [🎯 What is Kafka?](#-what-is-kafka)
  - [Key Features](#key-features)
  - [Kafka 4.0 New Features](#kafka-40-new-features)
  - [Advantages & Trade-offs](#advantages--trade-offs)
  - [When to Use Kafka](#when-to-use-kafka)
- [🏗️ Architecture Deep Dive](#️-architecture-deep-dive)
- [🚀 Getting Started](#-getting-started)
- [🐳 Docker Deployment](#-docker-deployment)
- [☸️ Kubernetes Deployment](#️-kubernetes-deployment)
- [📚 Client Libraries & SDKs](#-client-libraries--sdks)
- [⚡ Performance & Optimization](#-performance--optimization)
- [📊 Monitoring & Observability](#-monitoring--observability)
- [🆚 Kafka vs RabbitMQ vs Redis](#-kafka-vs-rabbitmq-vs-redis)
- [💡 Use Cases & Patterns](#-use-cases--patterns)
- [🌟 Awesome Projects](#-awesome-projects)
- [📖 Learning Resources](#-learning-resources)
- [🤝 Contributing](#-contributing)

---

## 🎯 What is Kafka?

**Apache Kafka** is an open-source distributed event streaming platform used by thousands of companies for high-performance data pipelines, streaming analytics, data integration, and mission-critical applications.

### Key Features

- **📈 High Throughput**: Handle millions of messages per second with low latency
- **🔄 Distributed Architecture**: Horizontally scalable across multiple nodes
- **💾 Persistent Storage**: Durable message storage on disk with configurable retention
- **🔁 Message Replay**: Consume historical data from any point in time
- **🌐 Multi-Protocol Support**: Native Kafka protocol, REST, JDBC, and more
- **🛡️ Fault Tolerance**: Automatic failover and data replication
- **⚡ Real-Time Processing**: Stream processing with Kafka Streams API
- **🔌 Rich Ecosystem**: 100+ connectors via Kafka Connect

### Kafka 4.0 New Features (March 2025)

<details open>
<parameter name="summary"><b>🆕 What's New in Kafka 4.0</b></summary>

#### 1️⃣ **ZooKeeper Removal - KRaft is Now Default**

Kafka 4.0 **completely removes ZooKeeper dependency**, making KRaft (Kafka Raft) the default consensus protocol.

**Benefits:**
- ✅ Simplified operations (no ZooKeeper cluster to manage)
- ✅ Faster metadata operations (10x improvement)
- ✅ Better scalability (millions of partitions)
- ✅ Reduced operational complexity

```bash
# KRaft mode is now default - no ZooKeeper needed!
# Old way (pre-4.0): Required separate ZooKeeper ensemble
# New way (4.0+): Pure Kafka cluster
```

#### 2️⃣ **Next-Generation Consumer Rebalance Protocol**

**Problem Solved:** Traditional "stop-the-world" rebalances caused downtime

**New Protocol Benefits:**
- 🚀 **Zero-downtime rebalances** - consumers keep processing
- 📊 **Better performance** in large deployments (1000+ consumers)
- ⏱️ **Reduced latency** during group changes
- 🎯 **Incremental rebalancing** instead of full reassignment

#### 3️⃣ **Queue Support (Preview Feature)**

**KIP-932** introduces traditional message queue capabilities:

```java
// New Queue API
KafkaQueue<String, Order> queue = new KafkaQueue<>(configs);

// Individual message acknowledgment (not just offset commit)
queue.consume(record -> {
    processOrder(record.value());
    record.acknowledge(); // Individual ack!
});

// Unordered processing with parallelism
queue.setParallelism(10);
```

**Features:**
- ✅ Individual message acknowledgments
- ✅ Message redelivery on failure
- ✅ Unordered parallel processing
- ✅ Competes with RabbitMQ/SQS use cases

#### 4️⃣ **Java Version Updates**

- **Clients & Streams**: Requires **Java 11+**
- **Brokers & Connect**: Requires **Java 17+**

#### 5️⃣ **Pre-Vote Mechanism (KIP-996)**

Reduces unnecessary leader elections in KRaft clusters for better stability.

</details>

### Advantages

| Feature | Benefit |
|---------|---------|
| ⚡ **Ultra-High Throughput** | 1M+ messages/second per broker |
| 💾 **Persistent Storage** | Messages stored on disk, not just memory |
| 🔁 **Message Replay** | Re-consume from any point in time |
| 📈 **Horizontal Scalability** | Add brokers to scale linearly |
| 🌍 **Geo-Replication** | Multi-datacenter disaster recovery |
| 🔒 **Exactly-Once Semantics** | Strong delivery guarantees |
| 🎯 **Partitioning** | Built-in parallelism and ordering |
| 🔧 **Rich Ecosystem** | Streams, Connect, ksqlDB, Schema Registry |
| 📊 **Event Sourcing** | Natural fit for event-driven architectures |
| 💪 **Battle-Tested** | Used by 80% of Fortune 100 companies |

### Trade-offs

| Consideration | Details |
|---------------|---------|
| 🧠 **Learning Curve** | Steeper than traditional message queues |
| 🔧 **Operational Complexity** | More complex to operate than RabbitMQ |
| 💻 **Resource Usage** | Higher memory/disk requirements |
| 🎯 **Over-Engineering** | Overkill for simple pub/sub use cases |
| 📝 **Configuration** | Many tuning parameters to understand |
| 💰 **Cost** | Higher infrastructure costs for small scale |

### When to Use Kafka

#### ✅ Perfect For:

- **Event Streaming & Processing**: Real-time data pipelines
- **Log Aggregation**: Centralized logging at scale
- **Metrics & Monitoring**: Time-series data collection
- **Change Data Capture (CDC)**: Database replication
- **Event Sourcing**: Immutable event store
- **Microservices Communication**: Event-driven architecture
- **Real-Time Analytics**: Stream processing with Kafka Streams
- **Message Replay**: Need to reprocess historical data
- **High-Throughput Scenarios**: Millions of events/second

#### ❌ Not Ideal For:

- Simple request/response (use REST API)
- Low-latency requirements <1ms (use Redis)
- Small-scale applications (<10K msgs/day)
- Complex message routing (use RabbitMQ)
- When operational simplicity is critical
- Short-lived messages only

---

## 🏗️ Architecture Deep Dive

### Core Components

```
┌─────────────────────────────────────────────────────────────┐
│                      Kafka Cluster                          │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌────────────┐  ┌────────────┐  ┌────────────┐          │
│  │  Broker 1  │  │  Broker 2  │  │  Broker 3  │          │
│  │            │  │            │  │            │          │
│  │ Topic A    │  │ Topic A    │  │ Topic B    │          │
│  │ - Part 0   │  │ - Part 1   │  │ - Part 0   │          │
│  │ - Part 2   │  │            │  │ - Part 1   │          │
│  └────────────┘  └────────────┘  └────────────┘          │
│                                                             │
│  ┌──────────────────────────────────────────────┐          │
│  │         KRaft Controllers (No ZooKeeper!)    │          │
│  │  - Metadata Management                       │          │
│  │  - Leader Election                           │          │
│  └──────────────────────────────────────────────┘          │
└─────────────────────────────────────────────────────────────┘

         ▲                                    │
         │ Produce                  Consume   │
         │                                    ▼

┌─────────────────┐              ┌─────────────────┐
│   Producers     │              │   Consumers     │
│                 │              │                 │
│ - App Server    │              │ - Analytics     │
│ - IoT Devices   │              │ - Microservices │
│ - Databases     │              │ - Streams App   │
└─────────────────┘              └─────────────────┘
```

### Topics & Partitions

**Topics**: Categories or feed names to which records are published

**Partitions**: Ordered, immutable sequence of records within a topic

```
Topic: "user-events"
├─ Partition 0: [msg0, msg3, msg6, msg9]  (ordered within partition)
├─ Partition 1: [msg1, msg4, msg7, msg10]
└─ Partition 2: [msg2, msg5, msg8, msg11]

Key: user_id=123 → Always goes to same partition (ordering guaranteed)
```

**Why Partitions?**
- ✅ **Parallelism**: Multiple consumers process different partitions
- ✅ **Scalability**: Distribute data across brokers
- ✅ **Ordering**: Guarantee order within partition
- ✅ **Throughput**: Write/read in parallel

### Producers

**Responsibility**: Publish records to Kafka topics

```python
# Producer with key for partitioning
producer.send(
    topic='user-events',
    key=user_id,        # Same key → same partition
    value=event_data,
    headers={'source': 'web-app'}
)
```

**Key Features:**
- **Batching**: Combine multiple records for efficiency
- **Compression**: LZ4, Snappy, GZIP, ZSTD
- **Partitioning**: Hash-based, round-robin, or custom
- **Idempotence**: Exactly-once delivery semantics

### Consumers & Consumer Groups

**Consumer**: Application that reads from Kafka topics

**Consumer Group**: Multiple consumers working together

```
Consumer Group: "analytics-service"

Topic: "events" (3 partitions)
├─ Partition 0 → Consumer A (reads P0)
├─ Partition 1 → Consumer B (reads P1)
└─ Partition 2 → Consumer C (reads P2)

Parallelism = min(consumers, partitions)
```

**Features:**
- **Automatic Rebalancing**: Redistribute partitions on consumer changes
- **Offset Management**: Track processing position
- **At-least-once / Exactly-once**: Configurable semantics

### Replication

```
Topic: "critical-data" (replication-factor=3)

Broker 1: [Partition 0 - Leader]
Broker 2: [Partition 0 - Replica]
Broker 3: [Partition 0 - Replica]

Leader: Handles all reads/writes
Replicas: Sync data from leader (ISR - In-Sync Replicas)
```

**Fault Tolerance:**
- Leader fails → Automatic failover to replica
- min.insync.replicas=2 → Requires 2 replicas before ack
- Prevents data loss in broker failures

---

## 🚀 Getting Started

### Quick Start (Docker)

```bash
# 1. Start Kafka in KRaft mode (no ZooKeeper!)
docker run -d \
  --name kafka \
  -p 9092:9092 \
  apache/kafka:latest

# 2. Create a topic
docker exec kafka /opt/kafka/bin/kafka-topics.sh \
  --create \
  --topic quickstart-events \
  --bootstrap-server localhost:9092 \
  --partitions 3 \
  --replication-factor 1

# 3. Producer - Send messages
docker exec -it kafka /opt/kafka/bin/kafka-console-producer.sh \
  --topic quickstart-events \
  --bootstrap-server localhost:9092

# 4. Consumer - Read messages
docker exec -it kafka /opt/kafka/bin/kafka-console-consumer.sh \
  --topic quickstart-events \
  --from-beginning \
  --bootstrap-server localhost:9092
```

### Installation (Local)

<details>
<parameter name="summary"><b>📦 Local Installation</b></summary>

```bash
# Download Kafka 4.0
wget https://downloads.apache.org/kafka/4.0.0/kafka_2.13-4.0.0.tgz
tar -xzf kafka_2.13-4.0.0.tgz
cd kafka_2.13-4.0.0

# Start Kafka in KRaft mode
KAFKA_CLUSTER_ID="$(bin/kafka-storage.sh random-uuid)"

bin/kafka-storage.sh format \
  -t $KAFKA_CLUSTER_ID \
  -c config/kraft/server.properties

bin/kafka-server-start.sh config/kraft/server.properties
```

</details>

---

## 🐳 Docker Deployment

### Production Docker Compose

```yaml
version: '3.8'

services:
  kafka:
    image: apache/kafka:4.0.0
    container_name: kafka
    ports:
      - "9092:9092"
      - "9093:9093"
    environment:
      # KRaft Configuration (No ZooKeeper!)
      KAFKA_NODE_ID: 1
      KAFKA_PROCESS_ROLES: 'broker,controller'
      KAFKA_CONTROLLER_QUORUM_VOTERS: '1@kafka:9093'
      KAFKA_LISTENERS: 'PLAINTEXT://kafka:9092,CONTROLLER://kafka:9093'
      KAFKA_ADVERTISED_LISTENERS: 'PLAINTEXT://localhost:9092'
      KAFKA_CONTROLLER_LISTENER_NAMES: 'CONTROLLER'

      # Performance Tuning
      KAFKA_NUM_PARTITIONS: 3
      KAFKA_DEFAULT_REPLICATION_FACTOR: 1
      KAFKA_MIN_INSYNC_REPLICAS: 1
      KAFKA_LOG_RETENTION_HOURS: 168
      KAFKA_LOG_SEGMENT_BYTES: 1073741824

      # Memory & Resources
      KAFKA_HEAP_OPTS: "-Xmx2G -Xms2G"

    volumes:
      - kafka_data:/var/lib/kafka/data
    healthcheck:
      test: ["CMD", "kafka-broker-api-versions.sh", "--bootstrap-server", "localhost:9092"]
      interval: 10s
      timeout: 5s
      retries: 5

  kafka-ui:
    image: provectuslabs/kafka-ui:latest
    ports:
      - "8080:8080"
    environment:
      KAFKA_CLUSTERS_0_NAME: local
      KAFKA_CLUSTERS_0_BOOTSTRAPSERVERS: kafka:9092
    depends_on:
      - kafka

volumes:
  kafka_data:
```

---

## ☸️ Kubernetes Deployment

### Strimzi Operator (Recommended)

```bash
# Install Strimzi Operator
kubectl create namespace kafka
kubectl create -f 'https://strimzi.io/install/latest?namespace=kafka' -n kafka

# Wait for operator to be ready
kubectl wait --for=condition=ready pod -l name=strimzi-cluster-operator -n kafka --timeout=300s
```

### Deploy Kafka Cluster

```yaml
# kafka-cluster.yaml
apiVersion: kafka.strimzi.io/v1beta2
kind: Kafka
metadata:
  name: production-cluster
  namespace: kafka
spec:
  kafka:
    version: 4.0.0
    replicas: 3

    listeners:
      - name: plain
        port: 9092
        type: internal
        tls: false
      - name: tls
        port: 9093
        type: internal
        tls: true

    config:
      offsets.topic.replication.factor: 3
      transaction.state.log.replication.factor: 3
      transaction.state.log.min.isr: 2
      default.replication.factor: 3
      min.insync.replicas: 2
      inter.broker.protocol.version: "4.0"

      # Performance
      num.partitions: 3
      compression.type: lz4
      log.retention.hours: 168
      log.segment.bytes: 1073741824

    storage:
      type: jbod
      volumes:
        - id: 0
          type: persistent-claim
          size: 100Gi
          class: fast-ssd
          deleteClaim: false

    resources:
      requests:
        memory: 4Gi
        cpu: "2"
      limits:
        memory: 8Gi
        cpu: "4"

  # KRaft Mode (No ZooKeeper needed in Kafka 4.0!)
  # entityOperator section can be omitted for pure KRaft

  kafkaExporter:
    topicRegex: ".*"
    groupRegex: ".*"
```

```bash
# Deploy cluster
kubectl apply -f kafka-cluster.yaml

# Check status
kubectl get kafka -n kafka
kubectl get pods -n kafka
```

### Helm Chart (Alternative)

```bash
# Add Bitnami repository
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update

# Install Kafka
helm install kafka bitnami/kafka \
  --set replicaCount=3 \
  --set persistence.size=100Gi \
  --set metrics.kafka.enabled=true \
  --set metrics.jmx.enabled=true \
  --set metrics.serviceMonitor.enabled=true \
  --namespace kafka
```

---

## 📚 Client Libraries & SDKs

### Java (Official)

```xml
<!-- Maven -->
<dependency>
    <groupId>org.apache.kafka</groupId>
    <artifactId>kafka-clients</artifactId>
    <version>4.0.0</version>
</dependency>
```

```java
// Producer Example
Properties props = new Properties();
props.put("bootstrap.servers", "localhost:9092");
props.put("key.serializer", "org.apache.kafka.common.serialization.StringSerializer");
props.put("value.serializer", "org.apache.kafka.common.serialization.StringSerializer");
props.put("acks", "all");
props.put("retries", 3);

KafkaProducer<String, String> producer = new KafkaProducer<>(props);

ProducerRecord<String, String> record =
    new ProducerRecord<>("my-topic", "key", "value");

producer.send(record, (metadata, exception) -> {
    if (exception == null) {
        System.out.println("Sent to partition " + metadata.partition());
    }
});

producer.close();
```

### Python

**confluent-kafka-python** (Recommended - backed by librdkafka)

```bash
pip install confluent-kafka
```

```python
from confluent_kafka import Producer, Consumer

# Producer
producer = Producer({'bootstrap.servers': 'localhost:9092'})

def delivery_report(err, msg):
    if err:
        print(f'Delivery failed: {err}')
    else:
        print(f'Message delivered to {msg.topic()} [{msg.partition()}]')

producer.produce('my-topic', value='Hello Kafka', callback=delivery_report)
producer.flush()

# Consumer
consumer = Consumer({
    'bootstrap.servers': 'localhost:9092',
    'group.id': 'my-group',
    'auto.offset.reset': 'earliest'
})

consumer.subscribe(['my-topic'])

while True:
    msg = consumer.poll(1.0)
    if msg is None:
        continue
    if msg.error():
        print(f"Error: {msg.error()}")
    else:
        print(f"Received: {msg.value().decode('utf-8')}")

consumer.close()
```

**kafka-python** (Pure Python - Alternative)

```bash
pip install kafka-python
```

### Node.js

**Confluent's JavaScript Client** (Recommended - GA in 2025)

```bash
npm install @confluentinc/kafka-javascript
```

```javascript
const { Kafka } = require('@confluentinc/kafka-javascript');

const kafka = new Kafka({
  'bootstrap.servers': 'localhost:9092'
});

// Producer
const producer = kafka.producer();
await producer.connect();

await producer.send({
  topic: 'my-topic',
  messages: [
    { key: 'key1', value: 'Hello Kafka from Node.js!' }
  ]
});

// Consumer
const consumer = kafka.consumer({ 'group.id': 'my-group' });
await consumer.connect();
await consumer.subscribe({ topics: ['my-topic'] });

await consumer.run({
  eachMessage: async ({ topic, partition, message }) => {
    console.log({
      value: message.value.toString(),
      partition: partition
    });
  }
});
```

### Go

**sarama** (Most popular)

```bash
go get github.com/IBM/sarama
```

```go
package main

import (
    "github.com/IBM/sarama"
    "log"
)

func main() {
    // Producer
    config := sarama.NewConfig()
    config.Producer.Return.Successes = true

    producer, err := sarama.NewSyncProducer([]string{"localhost:9092"}, config)
    if err != nil {
        log.Fatal(err)
    }
    defer producer.Close()

    msg := &sarama.ProducerMessage{
        Topic: "my-topic",
        Value: sarama.StringEncoder("Hello from Go!"),
    }

    partition, offset, err := producer.SendMessage(msg)
    log.Printf("Message sent to partition %d at offset %d\n", partition, offset)
}
```

---

## ⚡ Performance & Optimization

### Producer Optimization

```python
# High-Throughput Producer Configuration
producer_config = {
    'bootstrap.servers': 'localhost:9092',

    # Batching (crucial for throughput)
    'batch.size': 100000,           # 100KB batches (default: 16KB)
    'linger.ms': 10,                # Wait 10ms to fill batch

    # Compression
    'compression.type': 'lz4',      # Fast compression (snappy, gzip, zstd)

    # Reliability vs Performance
    'acks': 1,                      # 0=no ack, 1=leader, all=all replicas
    'retries': 3,
    'max.in.flight.requests.per.connection': 5,

    # Buffer
    'buffer.memory': 67108864,      # 64MB buffer
}
```

**Throughput Impact:**
```
Default config:    ~23 MB/sec
Optimized config:  ~95 MB/sec (4x improvement!)
```

### Consumer Optimization

```python
consumer_config = {
    'bootstrap.servers': 'localhost:9092',
    'group.id': 'high-perf-group',

    # Fetch Settings
    'fetch.min.bytes': 50000,       # Min data before fetch
    'fetch.max.wait.ms': 500,       # Max wait for min bytes
    'max.partition.fetch.bytes': 1048576,  # 1MB per partition

    # Parallel Processing
    'max.poll.records': 500,        # Records per poll

    # Offset Management
    'enable.auto.commit': False,    # Manual commit for exactly-once
    'auto.offset.reset': 'earliest'
}
```

### Broker Tuning

```properties
# server.properties

# Network Threads (8-16 cores)
num.network.threads=8
num.io.threads=16

# Log Settings
log.segment.bytes=1073741824       # 1GB segments
log.retention.hours=168            # 7 days
log.retention.check.interval.ms=300000

# Replication
num.replica.fetchers=4
replica.lag.time.max.ms=30000

# Performance
compression.type=lz4
min.insync.replicas=2
unclean.leader.election.enable=false
```

### Partitioning Strategy

```
Rule of Thumb:
Partitions = max(target_throughput / partition_throughput, consumer_parallelism)

Example:
Target: 100K msgs/sec
Per partition: 10K msgs/sec
Partitions needed: 10

Consumers: 10 (one per partition for max parallelism)
```

---

## 📊 Monitoring & Observability

### Prometheus + Grafana Setup

```yaml
# kafka-monitoring.yaml
apiVersion: v1
kind: Service
metadata:
  name: kafka-metrics
  labels:
    app: kafka
spec:
  ports:
  - name: metrics
    port: 9308
    targetPort: 9308
  selector:
    app: kafka
---
apiVersion: monitoring.coreos.com/v1
kind: ServiceMonitor
metadata:
  name: kafka-metrics
spec:
  selector:
    matchLabels:
      app: kafka
  endpoints:
  - port: metrics
    interval: 30s
```

### Key Metrics to Monitor

| Metric | Alert Threshold | Description |
|--------|----------------|-------------|
| `kafka_server_replicamanager_underreplicatedpartitions` | > 0 | Partitions without full replicas |
| `kafka_server_brokerstate` | != 3 | Broker not in running state |
| `kafka_server_replicamanager_leadercount` | Unbalanced | Leader distribution |
| `kafka_server_brokertopicmetrics_messagesinpersec` | Sudden drop | Incoming message rate |
| `kafka_consumer_group_lag` | > 10000 | Consumer lag |
| `kafka_server_replicafetchermanager_minfetchrate` | < 1 | Replication issues |

### Grafana Dashboards

**Pre-built dashboards:**
- [Kafka Overview](https://grafana.com/grafana/dashboards/11962-kafka-metrics/)
- [Kafka Exporter](https://grafana.com/grafana/dashboards/7589-kafka-exporter/)
- [Strimzi Kafka](https://grafana.com/grafana/dashboards/11826-strimzi-kafka/)

---

## 🆚 Kafka vs RabbitMQ vs Redis

### Comprehensive Comparison

| Feature | Apache Kafka | RabbitMQ | Redis |
|---------|--------------|----------|-------|
| **Throughput** | 1M+ msgs/sec | ~50K msgs/sec | ~100K msgs/sec |
| **Latency** | 5-10ms (p99) | 1-5ms | <1ms |
| **Persistence** | Disk-based, long-term | Optional, short-term | In-memory, optional dump |
| **Message Retention** | Days/weeks/forever | Until consumed | No retention |
| **Message Replay** | ✅ Yes (time-based) | ❌ No | ❌ No |
| **Ordering** | Per partition | Per queue | Per channel |
| **Scalability** | Excellent (horizontal) | Good (vertical) | Good (cluster) |
| **Use Case** | Event streaming, logs | Task queues, RPC | Cache, pub/sub |
| **Protocol** | Binary (custom) | AMQP, MQTT, STOMP | Redis protocol |
| **Complexity** | High | Medium | Low |
| **Best For** | Big data, analytics | Microservices | Real-time, low latency |

### When to Use What

```
Choose Kafka when:
✅ High throughput (>100K msgs/sec)
✅ Need to replay messages
✅ Event sourcing / CQRS
✅ Stream processing
✅ Log aggregation
✅ Long-term message retention

Choose RabbitMQ when:
✅ Complex routing required
✅ Traditional message queue patterns
✅ Priority queues needed
✅ Lower throughput (<50K msgs/sec)
✅ Simple to operate is priority
✅ Multi-protocol support

Choose Redis when:
✅ Ultra-low latency (<1ms)
✅ Simple pub/sub
✅ Also need caching
✅ Short-lived messages
✅ Fire-and-forget messaging
```

---

## 💡 Use Cases & Patterns

### 1. Real-Time Analytics

```python
# Kafka Streams for real-time analytics
from kafka import KafkaConsumer, KafkaProducer
import json

# Consume clickstream events
consumer = KafkaConsumer(
    'clickstream',
    bootstrap_servers=['localhost:9092'],
    value_deserializer=lambda m: json.loads(m.decode('utf-8'))
)

# Aggregate views per user
user_views = {}

for message in consumer:
    event = message.value
    user_id = event['user_id']
    user_views[user_id] = user_views.get(user_id, 0) + 1

    # Publish aggregated metrics
    if user_views[user_id] % 10 == 0:  # Every 10 views
        producer.send('user-analytics', {
            'user_id': user_id,
            'total_views': user_views[user_id]
        })
```

### 2. Microservices Event Bus

```
Order Service → Kafka("order.created") → [Inventory, Payment, Notification]

Topic: order-events
├─ order.created
├─ order.updated
├─ order.completed
└─ order.cancelled

Each microservice consumes relevant events independently
```

### 3. Log Aggregation

```
Application Servers (100s) → Kafka → [Elasticsearch, S3, Analytics]

Benefits:
- Decouples log producers from consumers
- Buffering during consumer downtime
- Multiple consumers for different purposes
- Replay logs for debugging
```

### 4. Change Data Capture (CDC)

```sql
-- Database changes streamed to Kafka
PostgreSQL → Debezium → Kafka → [Search Index, Cache, Analytics]

Topic: db.public.users
- INSERT: {"op":"c","after":{"id":1,"name":"Alice"}}
- UPDATE: {"op":"u","before":{...},"after":{...}}
- DELETE: {"op":"d","before":{"id":1}}
```

---

## 🌟 Awesome Projects

### Curated Lists

| Repository | Description | Stars |
|------------|-------------|-------|
| [awesome-kafka](https://github.com/semantalytics/awesome-kafka) | Curated list of Kafka resources | ![Stars](https://img.shields.io/github/stars/semantalytics/awesome-kafka?style=social) |
| [awesome-opensource-contribs-kafka](https://github.com/streamthoughts/awesome-opensource-contribs-kafka) | Open-source Kafka contributions | ![Stars](https://img.shields.io/github/stars/streamthoughts/awesome-opensource-contribs-kafka?style=social) |

### Production Tools

| Tool | Description | Use Case |
|------|-------------|----------|
| [AKHQ](https://github.com/tchiotludo/akhq) | Kafka GUI for Apache Kafka | Management & Monitoring |
| [Cruise Control](https://github.com/linkedin/cruise-control) | Auto workload rebalancing | Auto-scaling |
| [Burrow](https://github.com/linkedin/Burrow) | Consumer lag monitoring | Alerting |
| [Kafdrop](https://github.com/obsidiandynamics/kafdrop) | Web UI for Kafka | Visualization |

### Example Projects

| Project | Description |
|---------|-------------|
| [kafka-streams-ml-examples](https://github.com/kaiwaehner/kafka-streams-machine-learning-examples) | ML models with Kafka Streams |
| [kafka-connect-examples](https://github.com/confluentinc/demo-scene) | Kafka Connect demos |

---

## 📖 Learning Resources

### Official Documentation

- [Apache Kafka Documentation](https://kafka.apache.org/documentation/)
- [Confluent Platform](https://docs.confluent.io/)
- [Kafka Improvement Proposals (KIPs)](https://cwiki.apache.org/confluence/display/KAFKA/Kafka+Improvement+Proposals)

### Online Courses

| Platform | Course | Level |
|----------|--------|-------|
| **Confluent** | [Apache Kafka Fundamentals](https://developer.confluent.io/courses/) | Free, Beginner |
| **Udemy** | [Apache Kafka Series](https://www.udemy.com/topic/apache-kafka/) | 130K+ students |
| **Pluralsight** | [Kafka for Developers](https://www.pluralsight.com/) | Intermediate |
| **LinkedIn Learning** | [Kafka Essential Training](https://www.linkedin.com/learning/) | All levels |

### Books

1. **Kafka: The Definitive Guide** (2nd Edition, 2022)
2. **Kafka Streams in Action** (Manning)
3. **Designing Event-Driven Systems** (Free from Confluent)

### Certifications

- **Confluent Certified Developer for Apache Kafka (CCDAK)**
- **Confluent Certified Administrator for Apache Kafka (CCAAK)**

---

## 🤝 Contributing

This is an open-source community resource. Contributions welcome!

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

---

<div align="center">

### ⚡ Key Takeaways

**Apache Kafka is the de-facto standard for:**
- 🚀 High-throughput event streaming (1M+ msgs/sec)
- 💾 Durable message storage with replay capability
- 📊 Real-time stream processing and analytics
- 🌍 Distributed, fault-tolerant architectures
- 🔄 Event-driven microservices communication

**Used by 80% of Fortune 100 companies including:**
Netflix • LinkedIn • Uber • Airbnb • Spotify • Twitter

---

**Part of the Awesome Message Brokers Collection**

[← Back to Main README](README.md) | [AI Agents with Kafka →](KAFKA-AI-AGENTS.md)

</div>
