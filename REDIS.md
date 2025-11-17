# 🚀 Complete Redis Guide - 2025 Edition

> **Ultra-fast in-memory data store, cache, and message broker**
> From basics to production deployment with Redis 8

[![Redis](https://img.shields.io/badge/Redis-8.0-DC382D?style=for-the-badge&logo=redis&logoColor=white)](https://redis.io)
[![Docker](https://img.shields.io/badge/Docker-Ready-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://hub.docker.com/_/redis)
[![Kubernetes](https://img.shields.io/badge/Kubernetes-Compatible-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)](https://kubernetes.io)

---

## 📋 Table of Contents

- [What is Redis?](#what-is-redis)
- [Redis 8 - Latest Features (2025)](#redis-8---latest-features-2025)
- [Architecture Deep Dive](#architecture-deep-dive)
- [Getting Started](#getting-started)
- [Deployment Options](#deployment-options)
- [Client Libraries](#client-libraries)
- [Data Structures](#data-structures)
- [Performance & Optimization](#performance--optimization)
- [Monitoring & Observability](#monitoring--observability)
- [Redis vs RabbitMQ vs Kafka](#redis-vs-rabbitmq-vs-kafka)
- [Use Cases & Patterns](#use-cases--patterns)
- [Awesome Projects](#awesome-projects)
- [Learning Resources](#learning-resources)

---

## 🎯 What is Redis?

**Redis** (Remote Dictionary Server) is an open-source, in-memory data structure store used as:
- **Database** - Persistent key-value store
- **Cache** - Ultra-fast data caching layer
- **Message Broker** - Pub/Sub messaging system
- **Streaming Engine** - Real-time data processing

### 🌟 Key Features

```
┌─────────────────────────────────────────┐
│          REDIS CORE FEATURES            │
├─────────────────────────────────────────┤
│ ⚡ In-Memory Speed  │ <1ms latency      │
│ 📊 Rich Data Types  │ 15+ structures    │
│ 🔄 Pub/Sub          │ Real-time msgs    │
│ 💾 Persistence      │ RDB + AOF         │
│ 🌐 Clustering       │ Auto sharding     │
│ 🔐 ACL Security     │ Fine-grained      │
│ 🤖 AI/ML Ready      │ Vector search     │
│ 📈 Scalability      │ 1M+ msgs/sec      │
└─────────────────────────────────────────┘
```

### ✅ Advantages

| Feature | Benefit |
|---------|---------|
| **Ultra-Low Latency** | Sub-millisecond response times (<1ms) |
| **High Throughput** | 1 million+ operations per second |
| **Versatile Data Types** | 15+ data structures (strings, hashes, streams, vectors) |
| **Persistence Options** | RDB snapshots + AOF logs for durability |
| **Atomic Operations** | All operations are atomic by default |
| **Pub/Sub Messaging** | Built-in real-time messaging |
| **Lua Scripting** | Server-side scripting for complex operations |
| **Clustering** | Automatic sharding and replication |
| **Active-Active Geo** | Multi-region deployments (Enterprise) |
| **JSON Support** | Native JSON handling with RedisJSON |
| **Search & Query** | Full-text search with RediSearch |
| **Vector Database** | AI/ML embeddings with RedisVL |

### ⚠️ Trade-offs

| Consideration | Details |
|---------------|---------|
| **Memory Limited** | Dataset must fit in RAM (or use Redis Flex for SSD) |
| **Single-Threaded** | Core operations run on single thread (I/O is threaded) |
| **Cost** | RAM is more expensive than disk storage |
| **Durability vs Speed** | Trade-off between persistence and performance |
| **Complexity** | Simple model but advanced features require expertise |
| **Cluster Limitations** | No multi-key operations across shards |

---

## 🚀 Redis 8 - Latest Features (2025)

Redis 8 GA was released with groundbreaking performance improvements!

### 📊 Performance Enhancements

```
REDIS 8 PERFORMANCE GAINS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Commands:        87% faster ████████░
Throughput:      2x increase ████████████████
Replication:     18% faster ███░
Memory:          30+ improvements ██████
Latency:         40% reduction ████░
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

### 🆕 Major Features

#### 1. **LangCache** - Semantic Caching for AI
```python
from langchain_redis import LangCache
from openai import OpenAI

# Initialize semantic cache
cache = LangCache(
    redis_url="redis://localhost:6379",
    ttl=3600,
    distance_threshold=0.1  # Similarity threshold
)

client = OpenAI()

# First call - cache miss
response = cache.get_or_create(
    prompt="Explain machine learning",
    model="gpt-4",
    callback=lambda: client.chat.completions.create(...)
)

# Similar call - cache hit! (saves API costs)
response2 = cache.get_or_create(
    prompt="What is ML?",  # Semantically similar
    model="gpt-4"
)
# Returns cached result - 100x faster, $0 cost
```

**Benefits:**
- ⚡ 100-1000x faster than API calls
- 💰 90%+ cost reduction on LLM calls
- 🎯 Semantic similarity matching
- 🔄 Automatic cache invalidation

#### 2. **Vector Sets** - New Data Type
```bash
# Create vector set with metadata
VSET.ADD products:embeddings product:1
  [0.1, 0.2, 0.3, ..., 0.768]
  JSON '{"name":"iPhone","price":999}'

# Similarity search
VSET.SEARCH products:embeddings
  [0.15, 0.21, 0.29, ...]
  TOPK 5
  DISTANCE cosine
```

#### 3. **Redis Flex** - Hybrid RAM/SSD
```yaml
# Store hot data in RAM, cold data on SSD
redis-server --enable-flex yes \
             --flex-storage-path /data/ssd \
             --flex-hot-threshold 0.8
```

**Use Cases:**
- 📚 Larger datasets (beyond RAM limits)
- 💰 Cost optimization (SSD is cheaper)
- ♨️ Hot/cold data separation

#### 4. **Enhanced Clustering**
- **Active-Active Geo-Distribution** - Multi-region writes
- **Improved Sharding** - Better distribution algorithms
- **Faster Failover** - <1 second recovery

#### 5. **Performance Improvements**
- **Multi-threaded I/O** - Better CPU utilization
- **Memory Optimizations** - 30+ memory efficiency improvements
- **Faster Replication** - 18% faster sync
- **Command Pipelining** - Optimized batch processing

---

## 🏗️ Architecture Deep Dive

### System Architecture

```
┌────────────────────────────────────────────────────────────┐
│                    CLIENT APPLICATIONS                      │
│         (Python, Node.js, Go, Java, .NET, etc.)            │
└────────────────────┬───────────────────────────────────────┘
                     │
        ┌────────────┴────────────┐
        │   REDIS PROTOCOL        │
        │   (RESP3/RESP2)         │
        └────────────┬────────────┘
                     │
┌────────────────────▼───────────────────────────────────────┐
│                  REDIS SERVER                               │
│  ┌──────────────────────────────────────────────────────┐  │
│  │           SINGLE-THREADED EVENT LOOP                 │  │
│  │  • Command Processing   • Lua Script Execution       │  │
│  │  • Key Expiration       • Replication                │  │
│  └──────────────────────────────────────────────────────┘  │
│                                                             │
│  ┌──────────────────────────────────────────────────────┐  │
│  │         MULTI-THREADED I/O LAYER (Redis 8)           │  │
│  │  • Network I/O          • Disk Writes                │  │
│  │  • Persistence          • Module Operations          │  │
│  └──────────────────────────────────────────────────────┘  │
└─────────────────────┬───────────────────────────────────────┘
                      │
         ┌────────────┼────────────┐
         │            │            │
    ┌────▼───┐   ┌───▼────┐  ┌───▼────┐
    │  RAM   │   │  RDB   │  │  AOF   │
    │(Primary)│   │(Snapsh)│  │ (Log)  │
    └────────┘   └────────┘  └────────┘
```

### Data Storage Model

```
┌─────────────────────────────────────────┐
│        IN-MEMORY KEY-VALUE STORE        │
├─────────────────────────────────────────┤
│  Key           │  Value (Data Struct)   │
├────────────────┼────────────────────────┤
│  user:1000     │  Hash: {name, email}   │
│  session:abc   │  String: JWT token     │
│  queue:tasks   │  List: [t1, t2, t3]    │
│  active:users  │  Set: {u1, u2, u3}     │
│  leaderboard   │  Sorted Set: rankings  │
│  events:stream │  Stream: time-series   │
│  product:vec   │  Vector: embeddings    │
└────────────────┴────────────────────────┘
```

### Persistence Mechanisms

#### RDB (Redis Database Backup)
```bash
# Point-in-time snapshots
save 900 1      # After 900 sec if ≥1 key changed
save 300 10     # After 300 sec if ≥10 keys changed
save 60 10000   # After 60 sec if ≥10000 keys changed
```

**Pros:** Compact, fast recovery, minimal impact
**Cons:** Data loss possible (up to save interval)

#### AOF (Append-Only File)
```bash
# Log every write operation
appendonly yes
appendfsync everysec   # Sync every second (good balance)
# appendfsync always   # Sync every write (safest, slowest)
# appendfsync no       # OS decides (fastest, least safe)
```

**Pros:** Minimal data loss, durable
**Cons:** Larger files, slower recovery

### Redis Cluster Architecture

```
┌─────────────────────────────────────────────────────────┐
│                   REDIS CLUSTER                         │
│              (16384 Hash Slots Total)                   │
└─────────────────────────────────────────────────────────┘
         │                  │                │
    ┌────▼────┐       ┌────▼────┐     ┌────▼────┐
    │ Master 1│       │ Master 2│     │ Master 3│
    │ Slots:  │       │ Slots:  │     │ Slots:  │
    │ 0-5460  │       │5461-10922│    │10923-16383│
    └────┬────┘       └────┬────┘     └────┬────┘
         │                 │                │
    ┌────▼────┐       ┌────▼────┐     ┌────▼────┐
    │Replica 1│       │Replica 2│     │Replica 3│
    │(Read-only)│     │(Read-only)│   │(Read-only)│
    └─────────┘       └─────────┘     └─────────┘

Auto failover: If Master 1 fails → Replica 1 promoted
Client routing: Clients redirect to correct shard
```

---

## 🚀 Getting Started

### Option 1: Docker (Fastest)

```bash
# Pull latest Redis 8 image
docker pull redis:latest

# Run Redis with persistence
docker run -d \
  --name redis \
  -p 6379:6379 \
  -v redis-data:/data \
  redis:latest redis-server --appendonly yes

# Test connection
docker exec -it redis redis-cli ping
# Output: PONG
```

#### Docker Compose with Monitoring

```yaml
version: '3.8'

services:
  redis:
    image: redis:8-alpine
    container_name: redis
    ports:
      - "6379:6379"
    volumes:
      - redis-data:/data
      - ./redis.conf:/usr/local/etc/redis/redis.conf
    command: redis-server /usr/local/etc/redis/redis.conf
    healthcheck:
      test: ["CMD", "redis-cli", "ping"]
      interval: 5s
      timeout: 3s
      retries: 5
    networks:
      - redis-network

  redis-commander:
    image: rediscommander/redis-commander:latest
    container_name: redis-ui
    environment:
      - REDIS_HOSTS=local:redis:6379
    ports:
      - "8081:8081"
    depends_on:
      - redis
    networks:
      - redis-network

  redis-exporter:
    image: oliver006/redis_exporter:latest
    container_name: redis-exporter
    ports:
      - "9121:9121"
    environment:
      - REDIS_ADDR=redis:6379
    depends_on:
      - redis
    networks:
      - redis-network

volumes:
  redis-data:

networks:
  redis-network:
    driver: bridge
```

**Launch stack:**
```bash
docker-compose up -d

# Access Redis Commander UI
open http://localhost:8081

# Check metrics
curl http://localhost:9121/metrics
```

### Option 2: Local Installation

#### macOS (Homebrew)
```bash
brew install redis
brew services start redis

# Test
redis-cli ping
```

#### Ubuntu/Debian
```bash
sudo apt update
sudo apt install redis-server

sudo systemctl enable redis-server
sudo systemctl start redis-server

# Verify
redis-cli ping
```

#### From Source (Latest Features)
```bash
wget https://download.redis.io/redis-stable.tar.gz
tar -xzvf redis-stable.tar.gz
cd redis-stable
make
sudo make install

# Run server
redis-server
```

### Basic Commands

```bash
# Start Redis CLI
redis-cli

# === STRING OPERATIONS ===
SET user:1000:name "Alice"
GET user:1000:name
# "Alice"

SETEX session:abc123 3600 "token_value"  # Expire in 1 hour
TTL session:abc123
# 3599

INCR counter:visits
# 1
INCRBY counter:visits 10
# 11

# === HASH OPERATIONS ===
HSET user:1000 name "Alice" email "alice@example.com" age 30
HGETALL user:1000
# 1) "name"
# 2) "Alice"
# 3) "email"
# 4) "alice@example.com"
# 5) "age"
# 6) "30"

HGET user:1000 email
# "alice@example.com"

# === LIST OPERATIONS ===
LPUSH queue:tasks "task1" "task2" "task3"
RPOP queue:tasks
# "task1"

LRANGE queue:tasks 0 -1
# 1) "task3"
# 2) "task2"

# === SET OPERATIONS ===
SADD online:users "user1" "user2" "user3"
SMEMBERS online:users
# 1) "user1"
# 2) "user2"
# 3) "user3"

SISMEMBER online:users "user1"
# 1 (true)

# === SORTED SET OPERATIONS ===
ZADD leaderboard 100 "player1" 250 "player2" 175 "player3"
ZRANGE leaderboard 0 -1 WITHSCORES
# 1) "player1"
# 2) "100"
# 3) "player3"
# 4) "175"
# 5) "player2"
# 6) "250"

ZREVRANGE leaderboard 0 2  # Top 3
# 1) "player2"
# 2) "player3"
# 3) "player1"

# === STREAM OPERATIONS ===
XADD events:clicks * user "user1" button "subscribe" timestamp "2025-01-15"
XREAD STREAMS events:clicks 0
```

---

## ☸️ Deployment Options

### Kubernetes with Redis Enterprise Operator

#### Install Redis Enterprise Operator

```bash
# Add Redis Enterprise Operator Helm repo
helm repo add redis https://raw.githubusercontent.com/RedisLabs/redis-enterprise-k8s-docs/master/
helm repo update

# Install operator
kubectl create namespace redis

helm install redis-enterprise redis/redis-enterprise-operator \
  --namespace redis \
  --set operator.image.tag=7.4.2-2
```

#### Deploy Redis Enterprise Cluster

```yaml
# redis-enterprise-cluster.yaml
apiVersion: app.redislabs.com/v1
kind: RedisEnterpriseCluster
metadata:
  name: redis-enterprise
  namespace: redis
spec:
  nodes: 3
  persistentSpec:
    enabled: true
    storageClassName: "fast-ssd"
    volumeSize: 100Gi
  redisEnterpriseNodeResources:
    limits:
      cpu: "4"
      memory: 16Gi
    requests:
      cpu: "2"
      memory: 8Gi
  redisEnterpriseImageSpec:
    imagePullPolicy: IfNotPresent
    repository: redislabs/redis
    versionTag: 7.4.2-92
  uiServiceType: LoadBalancer
```

```bash
kubectl apply -f redis-enterprise-cluster.yaml

# Check status
kubectl get rec -n redis
kubectl describe rec redis-enterprise -n redis
```

#### Create Redis Database

```yaml
# redis-database.yaml
apiVersion: app.redislabs.com/v1alpha1
kind: RedisEnterpriseDatabase
metadata:
  name: redis-db
  namespace: redis
spec:
  memorySize: 10GB
  shardCount: 3
  replication: true
  persistence: aofEverySecond
  modulesList:
    - name: search
      version: "2.8.4"
    - name: ReJSON
      version: "2.6.6"
    - name: bf
      version: "2.6.3"
  tlsMode: enabled
  proxyPolicy: all-master-shards
```

```bash
kubectl apply -f redis-database.yaml

# Get connection details
kubectl get secret redis-db -n redis -o jsonpath='{.data.password}' | base64 -d
kubectl get redb redis-db -n redis -o jsonpath='{.status.databaseURL}'
```

### Kubernetes with Helm (Community)

```bash
# Add Bitnami repo
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update

# Install Redis cluster
helm install redis bitnami/redis \
  --namespace redis \
  --create-namespace \
  --set architecture=replication \
  --set auth.password=yourpassword \
  --set master.persistence.enabled=true \
  --set master.persistence.size=10Gi \
  --set replica.replicaCount=2 \
  --set replica.persistence.enabled=true \
  --set replica.persistence.size=10Gi \
  --set metrics.enabled=true \
  --set metrics.serviceMonitor.enabled=true

# Get password
export REDIS_PASSWORD=$(kubectl get secret --namespace redis redis -o jsonpath="{.data.redis-password}" | base64 -d)

# Connect to Redis
kubectl run --namespace redis redis-client --restart='Never' \
  --env REDIS_PASSWORD=$REDIS_PASSWORD \
  --image docker.io/bitnami/redis:8.0 --command -- sleep infinity

kubectl exec --tty -i redis-client \
  --namespace redis -- bash

redis-cli -h redis-master -a $REDIS_PASSWORD
```

### Production Configuration

```conf
# redis.conf - Production settings

# NETWORK
bind 0.0.0.0
port 6379
tcp-backlog 511
timeout 0
tcp-keepalive 300

# SECURITY
requirepass your_strong_password_here
# ACL - Access Control Lists
aclfile /etc/redis/users.acl

# MEMORY
maxmemory 8gb
maxmemory-policy allkeys-lru  # Evict least recently used keys

# PERSISTENCE
save 900 1
save 300 10
save 60 10000
appendonly yes
appendfsync everysec
auto-aof-rewrite-percentage 100
auto-aof-rewrite-min-size 64mb

# REPLICATION
replica-read-only yes
repl-diskless-sync yes

# LOGGING
loglevel notice
logfile /var/log/redis/redis-server.log

# PERFORMANCE
lazyfree-lazy-eviction yes
lazyfree-lazy-expire yes
lazyfree-lazy-server-del yes

# CLUSTERING (if using cluster mode)
# cluster-enabled yes
# cluster-config-file nodes-6379.conf
# cluster-node-timeout 15000

# MODULES
# loadmodule /usr/lib/redis/modules/redisearch.so
# loadmodule /usr/lib/redis/modules/rejson.so
```

---

## 💻 Client Libraries

### Python - redis-py

```bash
pip install redis redis-om
```

```python
import redis
from redis.commands.json.path import Path

# Connect to Redis
r = redis.Redis(
    host='localhost',
    port=6379,
    password='yourpassword',
    decode_responses=True,  # Return strings instead of bytes
    socket_keepalive=True,
    socket_connect_timeout=5
)

# Test connection
r.ping()  # True

# === STRING OPERATIONS ===
r.set('user:1000:name', 'Alice', ex=3600)  # Expire in 1 hour
name = r.get('user:1000:name')  # 'Alice'

# === HASH OPERATIONS ===
r.hset('user:1000', mapping={
    'name': 'Alice',
    'email': 'alice@example.com',
    'age': 30
})
user = r.hgetall('user:1000')
# {'name': 'Alice', 'email': 'alice@example.com', 'age': '30'}

# === LIST OPERATIONS (Queue) ===
r.lpush('queue:tasks', 'task1', 'task2', 'task3')
task = r.rpop('queue:tasks')  # 'task1' (FIFO)

# === PUBSUB ===
pubsub = r.pubsub()
pubsub.subscribe('notifications')

# Publisher (in another connection)
r.publish('notifications', 'New message!')

# Subscriber
for message in pubsub.listen():
    if message['type'] == 'message':
        print(message['data'])
```

#### Redis-OM (Object Mapping)

```python
from redis_om import HashModel, Field
from typing import Optional

# Define model
class User(HashModel):
    name: str = Field(index=True)
    email: str = Field(index=True)
    age: int = Field(index=True)
    premium: bool = Field(default=False)

    class Meta:
        database = r

# Create user
user = User(
    name="Alice",
    email="alice@example.com",
    age=30,
    premium=True
)
user.save()

# Find users
premium_users = User.find(User.premium == True).all()
young_users = User.find(User.age < 25).all()

# Complex query
results = User.find(
    (User.age >= 25) & (User.premium == True)
).all()
```

### Node.js - node-redis

```bash
npm install redis
```

```javascript
import { createClient } from 'redis';

// Connect to Redis
const client = createClient({
  url: 'redis://localhost:6379',
  password: 'yourpassword',
  socket: {
    reconnectStrategy: (retries) => Math.min(retries * 50, 500)
  }
});

client.on('error', (err) => console.error('Redis Error:', err));
client.on('connect', () => console.log('Connected to Redis'));

await client.connect();

// === STRING OPERATIONS ===
await client.set('user:1000:name', 'Alice', { EX: 3600 });
const name = await client.get('user:1000:name');
console.log(name); // 'Alice'

// === HASH OPERATIONS ===
await client.hSet('user:1000', {
  name: 'Alice',
  email: 'alice@example.com',
  age: 30
});
const user = await client.hGetAll('user:1000');
console.log(user); // { name: 'Alice', email: 'alice@example.com', age: '30' }

// === LIST OPERATIONS ===
await client.lPush('queue:tasks', ['task1', 'task2', 'task3']);
const task = await client.rPop('queue:tasks');
console.log(task); // 'task1'

// === PUBSUB ===
const subscriber = client.duplicate();
await subscriber.connect();

await subscriber.subscribe('notifications', (message) => {
  console.log('Received:', message);
});

// Publish
await client.publish('notifications', 'New message!');

// === TRANSACTIONS ===
const multi = client.multi();
multi.set('key1', 'value1');
multi.set('key2', 'value2');
multi.incr('counter');
const results = await multi.exec();
console.log(results);

// === PIPELINE ===
const pipeline = client.multi();
for (let i = 0; i < 1000; i++) {
  pipeline.set(`key:${i}`, `value:${i}`);
}
await pipeline.exec();

await client.quit();
```

### Go - go-redis

```bash
go get github.com/redis/go-redis/v9
```

```go
package main

import (
    "context"
    "fmt"
    "github.com/redis/go-redis/v9"
    "time"
)

func main() {
    ctx := context.Background()

    // Connect to Redis
    rdb := redis.NewClient(&redis.Options{
        Addr:     "localhost:6379",
        Password: "yourpassword",
        DB:       0,
        PoolSize: 10,
    })

    // Test connection
    pong, err := rdb.Ping(ctx).Result()
    if err != nil {
        panic(err)
    }
    fmt.Println(pong) // "PONG"

    // === STRING OPERATIONS ===
    err = rdb.Set(ctx, "user:1000:name", "Alice", time.Hour).Err()
    if err != nil {
        panic(err)
    }

    name, err := rdb.Get(ctx, "user:1000:name").Result()
    if err != nil {
        panic(err)
    }
    fmt.Println(name) // "Alice"

    // === HASH OPERATIONS ===
    err = rdb.HSet(ctx, "user:1000", map[string]interface{}{
        "name":  "Alice",
        "email": "alice@example.com",
        "age":   30,
    }).Err()

    user, err := rdb.HGetAll(ctx, "user:1000").Result()
    fmt.Println(user) // map[name:Alice email:alice@example.com age:30]

    // === LIST OPERATIONS ===
    err = rdb.LPush(ctx, "queue:tasks", "task1", "task2", "task3").Err()
    task, err := rdb.RPop(ctx, "queue:tasks").Result()
    fmt.Println(task) // "task1"

    // === PUBSUB ===
    pubsub := rdb.Subscribe(ctx, "notifications")
    defer pubsub.Close()

    go func() {
        ch := pubsub.Channel()
        for msg := range ch {
            fmt.Println("Received:", msg.Payload)
        }
    }()

    // Publish
    err = rdb.Publish(ctx, "notifications", "New message!").Err()

    // === PIPELINE ===
    pipe := rdb.Pipeline()
    for i := 0; i < 1000; i++ {
        pipe.Set(ctx, fmt.Sprintf("key:%d", i), fmt.Sprintf("value:%d", i), 0)
    }
    _, err = pipe.Exec(ctx)

    // === TRANSACTIONS ===
    txf := func(tx *redis.Tx) error {
        _, err := tx.TxPipelined(ctx, func(pipe redis.Pipeliner) error {
            pipe.Set(ctx, "key1", "value1", 0)
            pipe.Set(ctx, "key2", "value2", 0)
            pipe.Incr(ctx, "counter")
            return nil
        })
        return err
    }

    err = rdb.Watch(ctx, txf, "key1", "key2")

    defer rdb.Close()
}
```

### Java - Jedis

```xml
<!-- pom.xml -->
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
    <version>5.1.0</version>
</dependency>
```

```java
import redis.clients.jedis.Jedis;
import redis.clients.jedis.JedisPool;
import redis.clients.jedis.JedisPoolConfig;
import redis.clients.jedis.Pipeline;

import java.util.Map;

public class RedisExample {
    public static void main(String[] args) {
        // Create connection pool
        JedisPoolConfig poolConfig = new JedisPoolConfig();
        poolConfig.setMaxTotal(128);
        poolConfig.setMaxIdle(128);
        poolConfig.setMinIdle(16);

        JedisPool pool = new JedisPool(poolConfig, "localhost", 6379);

        try (Jedis jedis = pool.getResource()) {
            // Set password if needed
            // jedis.auth("yourpassword");

            // Test connection
            String pong = jedis.ping();
            System.out.println(pong); // "PONG"

            // === STRING OPERATIONS ===
            jedis.setex("user:1000:name", 3600, "Alice");
            String name = jedis.get("user:1000:name");
            System.out.println(name); // "Alice"

            // === HASH OPERATIONS ===
            Map<String, String> user = Map.of(
                "name", "Alice",
                "email", "alice@example.com",
                "age", "30"
            );
            jedis.hset("user:1000", user);

            Map<String, String> userData = jedis.hgetAll("user:1000");
            System.out.println(userData);

            // === LIST OPERATIONS ===
            jedis.lpush("queue:tasks", "task1", "task2", "task3");
            String task = jedis.rpop("queue:tasks");
            System.out.println(task); // "task1"

            // === PIPELINE ===
            Pipeline pipeline = jedis.pipelined();
            for (int i = 0; i < 1000; i++) {
                pipeline.set("key:" + i, "value:" + i);
            }
            pipeline.sync();

        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            pool.close();
        }
    }
}
```

---

## 📊 Data Structures

Redis supports 15+ data structures. Here are the most important ones:

### 1. Strings
```bash
SET key "value"
GET key
INCR counter
DECR counter
APPEND key " more"
```
**Use Cases:** Caching, counters, session tokens

### 2. Hashes
```bash
HSET user:1000 name "Alice" email "alice@example.com"
HGET user:1000 name
HGETALL user:1000
HINCRBY user:1000 visits 1
```
**Use Cases:** Objects, user profiles, product details

### 3. Lists
```bash
LPUSH queue "task1"
RPUSH queue "task2"
LPOP queue
RPOP queue
LRANGE queue 0 -1
```
**Use Cases:** Queues, timelines, activity feeds

### 4. Sets
```bash
SADD tags "redis" "database" "nosql"
SMEMBERS tags
SISMEMBER tags "redis"  # 1 (true)
SUNION set1 set2
SINTER set1 set2
```
**Use Cases:** Tags, unique visitors, social graphs

### 5. Sorted Sets
```bash
ZADD leaderboard 100 "player1" 250 "player2"
ZRANGE leaderboard 0 -1 WITHSCORES
ZREVRANGE leaderboard 0 9  # Top 10
ZINCRBY leaderboard 50 "player1"
```
**Use Cases:** Leaderboards, ranking systems, time-series

### 6. Streams
```bash
XADD events * action "click" user "user1" timestamp "2025-01-15"
XREAD STREAMS events 0
XRANGE events - +
XGROUP CREATE events group1 0
XREADGROUP GROUP group1 consumer1 STREAMS events >
```
**Use Cases:** Event sourcing, real-time analytics, activity logs

### 7. Geospatial
```bash
GEOADD locations 13.361389 38.115556 "Palermo"
GEOADD locations 15.087269 37.502669 "Catania"
GEODIST locations "Palermo" "Catania" km  # 166.2742
GEORADIUS locations 15 37 200 km WITHDIST
```
**Use Cases:** Location-based services, proximity searches

### 8. HyperLogLog
```bash
PFADD unique:visitors "user1" "user2" "user3"
PFCOUNT unique:visitors  # 3
```
**Use Cases:** Unique counts with minimal memory (0.81% error rate)

### 9. Bitmaps
```bash
SETBIT user:activity:2025-01-15 1000 1  # User 1000 active
GETBIT user:activity:2025-01-15 1000  # 1
BITCOUNT user:activity:2025-01-15  # Total active users
```
**Use Cases:** Real-time analytics, feature flags

### 10. JSON (RedisJSON Module)
```bash
JSON.SET product:1 $ '{"name":"iPhone","price":999,"stock":50}'
JSON.GET product:1
JSON.NUMINCRBY product:1 $.stock -1
JSON.ARRAPPEND product:1 $.tags "5G" "OLED"
```
**Use Cases:** Complex objects, flexible schemas

---

## ⚡ Performance & Optimization

### Pipelining - Batch Commands

```python
import redis

r = redis.Redis()

# WITHOUT pipelining - 1000 round trips
for i in range(1000):
    r.set(f'key:{i}', f'value:{i}')
# ~1000ms

# WITH pipelining - 1 round trip
pipe = r.pipeline()
for i in range(1000):
    pipe.set(f'key:{i}', f'value:{i}')
pipe.execute()
# ~10ms (100x faster!)
```

### Connection Pooling

```python
import redis

# Create connection pool (reuse connections)
pool = redis.ConnectionPool(
    host='localhost',
    port=6379,
    max_connections=50,
    socket_keepalive=True,
    socket_connect_timeout=5,
    retry_on_timeout=True
)

r = redis.Redis(connection_pool=pool)
```

### Memory Optimization

```bash
# Use hashes for small objects (memory efficient)
# DON'T DO THIS (wasteful):
SET user:1000:name "Alice"
SET user:1000:email "alice@example.com"
SET user:1000:age "30"
# 3 keys = ~300 bytes overhead

# DO THIS (efficient):
HSET user:1000 name "Alice" email "alice@example.com" age "30"
# 1 key = ~100 bytes overhead (3x savings!)

# Configure hash encoding
redis-server --hash-max-ziplist-entries 512 \
             --hash-max-ziplist-value 64
```

### Eviction Policies

```conf
# redis.conf
maxmemory 8gb
maxmemory-policy allkeys-lru  # Choose one:

# allkeys-lru      - Evict least recently used (LRU) keys
# allkeys-lfu      - Evict least frequently used (LFU) keys
# volatile-lru     - Evict LRU keys with TTL set
# volatile-lfu     - Evict LFU keys with TTL set
# allkeys-random   - Evict random keys
# volatile-random  - Evict random keys with TTL
# volatile-ttl     - Evict keys with shortest TTL
# noeviction       - Return errors when memory full
```

### Performance Benchmarks

```bash
# Run Redis benchmark
redis-benchmark -h localhost -p 6379 -c 50 -n 100000

# Test specific commands
redis-benchmark -t set,get -n 100000 -q
# SET: 98039.22 requests per second
# GET: 102040.82 requests per second

# With pipelining
redis-benchmark -t set,get -n 100000 -P 16 -q
# SET: 1000000.00 requests per second (10x faster!)
# GET: 1250000.00 requests per second
```

### Slow Log Monitoring

```bash
# Configure slow log
CONFIG SET slowlog-log-slower-than 10000  # 10ms threshold
CONFIG SET slowlog-max-len 128

# Check slow queries
SLOWLOG GET 10
# 1) 1) (integer) 14     # Unique ID
#    2) (integer) 1618501234  # Timestamp
#    3) (integer) 12000   # Execution time (microseconds)
#    4) 1) "KEYS"         # Command
#       2) "user:*"
```

---

## 📈 Monitoring & Observability

### Prometheus + Grafana Stack

#### Redis Exporter Deployment

```yaml
# redis-exporter.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: redis-exporter
  namespace: redis
spec:
  replicas: 1
  selector:
    matchLabels:
      app: redis-exporter
  template:
    metadata:
      labels:
        app: redis-exporter
    spec:
      containers:
      - name: redis-exporter
        image: oliver006/redis_exporter:latest
        env:
        - name: REDIS_ADDR
          value: "redis-master:6379"
        - name: REDIS_PASSWORD
          valueFrom:
            secretKeyRef:
              name: redis
              key: redis-password
        ports:
        - containerPort: 9121
          name: metrics
---
apiVersion: v1
kind: Service
metadata:
  name: redis-exporter
  namespace: redis
  labels:
    app: redis-exporter
spec:
  ports:
  - port: 9121
    targetPort: 9121
    name: metrics
  selector:
    app: redis-exporter
---
apiVersion: monitoring.coreos.com/v1
kind: ServiceMonitor
metadata:
  name: redis-exporter
  namespace: redis
spec:
  selector:
    matchLabels:
      app: redis-exporter
  endpoints:
  - port: metrics
    interval: 30s
```

#### Key Metrics to Monitor

```promql
# Connection metrics
redis_connected_clients
redis_blocked_clients

# Memory metrics
redis_memory_used_bytes
redis_memory_max_bytes
redis_memory_fragmentation_ratio

# Performance metrics
rate(redis_commands_processed_total[5m])
redis_commands_duration_seconds_total

# Persistence metrics
redis_rdb_last_save_timestamp_seconds
redis_aof_last_rewrite_duration_seconds

# Replication metrics
redis_connected_slaves
redis_master_repl_offset
```

#### Grafana Dashboard

Import dashboard ID: **11835** (Redis Dashboard by Oliver006)

### Built-in Monitoring Commands

```bash
# Real-time monitoring
redis-cli --stat
# ------- data ------ --------------------- load -------------------- - child -
# keys       mem      clients blocked requests            connections
# 1000       1.5M     10      0       100000 (+0)         50

# Monitor all commands (debugging)
redis-cli MONITOR
# OK
# 1618501234.567890 [0 127.0.0.1:52134] "GET" "user:1000"
# 1618501234.890123 [0 127.0.0.1:52135] "SET" "session:abc" "token"

# Server info
INFO server
INFO memory
INFO stats
INFO replication
INFO cpu

# Client list
CLIENT LIST
# id=3 addr=127.0.0.1:52134 fd=8 name= age=12 idle=0 flags=N db=0 sub=0...

# Key space analysis
redis-cli --bigkeys
# Scanning the entire keyspace to find biggest keys
# [00.00%] Biggest string found so far 'user:1000:profile' with 1024 bytes
```

### Alerting Rules (Prometheus)

```yaml
# redis-alerts.yaml
groups:
- name: redis
  interval: 30s
  rules:
  - alert: RedisDown
    expr: redis_up == 0
    for: 1m
    labels:
      severity: critical
    annotations:
      summary: "Redis instance down"

  - alert: RedisHighMemory
    expr: redis_memory_used_bytes / redis_memory_max_bytes > 0.9
    for: 5m
    labels:
      severity: warning
    annotations:
      summary: "Redis memory usage > 90%"

  - alert: RedisHighConnections
    expr: redis_connected_clients > 1000
    for: 5m
    labels:
      severity: warning
    annotations:
      summary: "Redis has {{ $value }} connections"

  - alert: RedisReplicationLag
    expr: redis_master_repl_offset - redis_slave_repl_offset > 1000000
    for: 5m
    labels:
      severity: warning
    annotations:
      summary: "Redis replication lag detected"
```

---

## 🆚 Redis vs RabbitMQ vs Kafka

| Feature | Redis | RabbitMQ | Kafka |
|---------|-------|----------|-------|
| **Type** | In-memory DB/Cache/Broker | Message Broker | Event Streaming Platform |
| **Primary Use** | Caching, Real-time data | Task queues, RPC | Event streaming, Logs |
| **Performance** | **1M+ ops/sec** | 50K msgs/sec | 1M+ msgs/sec |
| **Latency** | **<1ms** (ultra-low) | ~5-10ms | ~10-20ms |
| **Storage** | **RAM** (+ SSD with Flex) | Disk + RAM | Disk (sequential writes) |
| **Persistence** | Optional (RDB + AOF) | Yes (durable queues) | Yes (log-based) |
| **Message Retention** | TTL-based | Consumed = deleted | Time/size-based retention |
| **Message Ordering** | Streams only | Yes (per queue) | Yes (per partition) |
| **Scalability** | Clustering (16K shards) | Clustering + Federation | **Partitioning** (unlimited) |
| **Replayability** | Streams only | No | **Yes** (key feature) |
| **Protocol** | RESP | AMQP, STOMP, MQTT | Custom binary protocol |
| **Pub/Sub** | Yes (fire-and-forget) | Yes (via exchanges) | Yes (consumer groups) |
| **Consumer Groups** | Streams only | Via queues | **Native support** |
| **Complexity** | **Low** | Medium | **High** |
| **Best For** | ⚡ Ultra-low latency<br>💾 Caching<br>🎮 Real-time apps<br>🔢 Counters | 📋 Task queues<br>🔄 RPC<br>📨 Message routing<br>🏢 Traditional messaging | 📊 Event sourcing<br>📈 Analytics<br>🔄 Stream processing<br>💾 Log aggregation |

### When to Use Each?

#### Use Redis When:
- ✅ You need **ultra-low latency** (<1ms)
- ✅ Caching is primary use case
- ✅ Data fits in memory (or use Redis Flex)
- ✅ Simple pub/sub is sufficient
- ✅ Real-time counters, leaderboards, session management
- ✅ AI semantic caching (LangCache)

#### Use RabbitMQ When:
- ✅ You need **complex routing** (topic, direct, fanout, headers)
- ✅ Task queue with acknowledgments
- ✅ RPC patterns (request/reply)
- ✅ Message priority and TTL
- ✅ Traditional enterprise messaging

#### Use Kafka When:
- ✅ You need **message replay** (event sourcing)
- ✅ Stream processing (real-time analytics)
- ✅ Log aggregation at scale
- ✅ Event-driven microservices
- ✅ High throughput (millions of msgs/sec)
- ✅ Long-term message retention

### Architecture Comparison

```
REDIS - In-Memory Data Store
┌──────────┐     ┌─────────────────┐
│ Client 1 │────▶│   Redis Server  │
│ Client 2 │────▶│   (RAM-based)   │
│ Client 3 │────▶│  Pub/Sub or DB  │
└──────────┘     └─────────────────┘
                        │
                   ┌────┴────┐
                   │   RDB   │
                   │   AOF   │
                   └─────────┘

RABBITMQ - Message Broker
┌───────────┐     ┌──────────┐     ┌──────────┐
│ Publisher │────▶│ Exchange │────▶│  Queue   │────▶ Consumer
└───────────┘     └──────────┘     └──────────┘
                       │
                  ┌────┴────┐
                  │ Routing │
                  │  Rules  │
                  └─────────┘

KAFKA - Event Streaming
┌───────────┐     ┌────────────────────┐     ┌──────────┐
│ Producer  │────▶│ Topic (Partitions) │────▶│ Consumer │
└───────────┘     │  [P1][P2][P3][P4] │     │  Group   │
                  └────────────────────┘     └──────────┘
                           │
                      ┌────┴─────┐
                      │   Disk   │
                      │(Sequential)│
                      └──────────┘
```

---

## 🎯 Use Cases & Patterns

### 1. Session Management

```python
import redis
import json
from datetime import timedelta

r = redis.Redis()

def create_session(user_id, data):
    session_id = generate_session_id()
    session_key = f"session:{session_id}"

    r.setex(
        session_key,
        timedelta(hours=24),
        json.dumps({
            'user_id': user_id,
            'data': data,
            'created_at': str(datetime.now())
        })
    )
    return session_id

def get_session(session_id):
    data = r.get(f"session:{session_id}")
    return json.loads(data) if data else None

def extend_session(session_id):
    r.expire(f"session:{session_id}", timedelta(hours=24))
```

### 2. Rate Limiting (Sliding Window)

```python
def check_rate_limit(user_id, limit=100, window=60):
    """Allow 100 requests per 60 seconds"""
    key = f"rate_limit:{user_id}"
    pipe = r.pipeline()
    now = time.time()

    # Remove old entries
    pipe.zremrangebyscore(key, 0, now - window)
    # Add current request
    pipe.zadd(key, {str(now): now})
    # Count requests in window
    pipe.zcard(key)
    # Set expiry
    pipe.expire(key, window)

    results = pipe.execute()
    request_count = results[2]

    return request_count <= limit
```

### 3. Distributed Locking (Redlock)

```python
import uuid

def acquire_lock(lock_name, timeout=10):
    """Distributed lock with auto-release"""
    identifier = str(uuid.uuid4())
    lock_key = f"lock:{lock_name}"

    # Try to acquire lock
    acquired = r.set(
        lock_key,
        identifier,
        nx=True,  # Only set if doesn't exist
        ex=timeout  # Auto-expire after timeout
    )

    return identifier if acquired else None

def release_lock(lock_name, identifier):
    """Release lock only if we own it"""
    lock_key = f"lock:{lock_name}"
    pipe = r.pipeline(True)

    while True:
        try:
            pipe.watch(lock_key)
            if pipe.get(lock_key) == identifier:
                pipe.multi()
                pipe.delete(lock_key)
                pipe.execute()
                return True
            pipe.unwatch()
            return False
        except redis.WatchError:
            continue

# Usage
lock_id = acquire_lock('resource:1')
if lock_id:
    try:
        # Critical section
        process_resource()
    finally:
        release_lock('resource:1', lock_id)
```

### 4. Caching Pattern (Cache-Aside)

```python
def get_user(user_id):
    """Cache-aside pattern"""
    cache_key = f"user:{user_id}"

    # Try cache first
    cached = r.get(cache_key)
    if cached:
        return json.loads(cached)

    # Cache miss - fetch from database
    user = db.query("SELECT * FROM users WHERE id = ?", user_id)

    # Store in cache
    if user:
        r.setex(cache_key, 3600, json.dumps(user))

    return user

def update_user(user_id, data):
    """Write-through pattern"""
    # Update database
    db.update("UPDATE users SET ... WHERE id = ?", data, user_id)

    # Invalidate cache
    r.delete(f"user:{user_id}")

    # Or update cache (write-through)
    # r.setex(f"user:{user_id}", 3600, json.dumps(data))
```

### 5. Leaderboard (Sorted Sets)

```python
def update_score(player_id, score):
    """Update player score"""
    r.zadd('leaderboard', {player_id: score})

def get_rank(player_id):
    """Get player rank (0-indexed)"""
    return r.zrevrank('leaderboard', player_id)

def get_top_players(n=10):
    """Get top N players"""
    return r.zrevrange('leaderboard', 0, n-1, withscores=True)

def get_around_player(player_id, radius=5):
    """Get players around specific player"""
    rank = r.zrevrank('leaderboard', player_id)
    if rank is None:
        return []

    start = max(0, rank - radius)
    end = rank + radius
    return r.zrevrange('leaderboard', start, end, withscores=True)
```

### 6. Real-time Analytics (HyperLogLog)

```python
def track_unique_visitor(page, user_id):
    """Count unique visitors with minimal memory"""
    key = f"unique:visitors:{page}:{date.today()}"
    r.pfadd(key, user_id)
    r.expire(key, 86400 * 30)  # Keep 30 days

def get_unique_count(page):
    """Get unique visitor count (0.81% error rate)"""
    key = f"unique:visitors:{page}:{date.today()}"
    return r.pfcount(key)

# Memory usage: ~12KB per HyperLogLog (vs millions in a set!)
```

### 7. Message Queue (Streams)

```python
def produce_event(stream_name, data):
    """Add event to stream"""
    r.xadd(stream_name, data, maxlen=10000)  # Keep last 10K events

def consume_events(stream_name, consumer_group, consumer_name):
    """Consume events with consumer group"""
    # Create consumer group (first time only)
    try:
        r.xgroup_create(stream_name, consumer_group, id='0', mkstream=True)
    except redis.ResponseError:
        pass  # Group already exists

    while True:
        # Read new messages
        messages = r.xreadgroup(
            consumer_group,
            consumer_name,
            {stream_name: '>'},
            count=10,
            block=1000  # Block for 1 second
        )

        for stream, events in messages:
            for event_id, data in events:
                try:
                    process_event(data)
                    # Acknowledge message
                    r.xack(stream_name, consumer_group, event_id)
                except Exception as e:
                    print(f"Error: {e}")
                    # Message remains unacked, will be redelivered
```

---

## 🌟 Awesome Projects

### Official Redis Projects

- **[Redis](https://github.com/redis/redis)** ⭐ 67K+ - Official Redis source code
- **[redis-py](https://github.com/redis/redis-py)** ⭐ 12K+ - Python client
- **[node-redis](https://github.com/redis/node-redis)** ⭐ 17K+ - Node.js client
- **[RedisInsight](https://github.com/RedisInsight/RedisInsight)** ⭐ 5K+ - GUI management tool
- **[redis-om-python](https://github.com/redis/redis-om-python)** ⭐ 1K+ - Object mapping

### Redis Modules

- **[RediSearch](https://github.com/RediSearch/RediSearch)** ⭐ 5K+ - Full-text search
- **[RedisJSON](https://github.com/RedisJSON/RedisJSON)** ⭐ 4K+ - JSON support
- **[RedisGraph](https://github.com/RedisGraph/RedisGraph)** ⭐ 2K+ - Graph database
- **[RedisTimeSeries](https://github.com/RedisTimeSeries/RedisTimeSeries)** ⭐ 1K+ - Time-series data
- **[RedisBloom](https://github.com/RedisBloom/RedisBloom)** ⭐ 2K+ - Probabilistic data structures
- **[RedisAI](https://github.com/RedisAI/RedisAI)** ⭐ 800+ - AI model serving

### Community Projects

- **[awesome-redis](https://github.com/JamzyWang/awesome-redis)** ⭐ 6K+ - Curated Redis resources
- **[bull](https://github.com/OptimalBits/bull)** ⭐ 15K+ - Premium Queue (Node.js)
- **[Celery](https://github.com/celery/celery)** ⭐ 24K+ - Distributed task queue (Python)
- **[Sidekiq](https://github.com/sidekiq/sidekiq)** ⭐ 13K+ - Background jobs (Ruby)
- **[Upstash](https://github.com/upstash/upstash-redis)** ⭐ 1K+ - Serverless Redis
- **[Redisson](https://github.com/redisson/redisson)** ⭐ 23K+ - Java client with advanced features

### Tools & Utilities

- **[redis-commander](https://github.com/joeferner/redis-commander)** ⭐ 3K+ - Web UI
- **[redis-exporter](https://github.com/oliver006/redis_exporter)** ⭐ 3K+ - Prometheus exporter
- **[redis-dump](https://github.com/delano/redis-dump)** ⭐ 2K+ - Backup/restore tool
- **[redis-rdb-tools](https://github.com/sripathikrishnan/redis-rdb-tools)** ⭐ 3K+ - RDB file parser
- **[Redis Desktop Manager](https://github.com/uglide/RedisDesktopManager)** ⭐ 23K+ - Desktop GUI

---

## 📚 Learning Resources

### Official Documentation

- **[Redis Official Docs](https://redis.io/docs/)** - Comprehensive documentation
- **[Redis Commands Reference](https://redis.io/commands/)** - All commands with examples
- **[Redis University](https://university.redis.com/)** - Free courses
- **[Redis Best Practices](https://redis.io/docs/manual/patterns/)** - Design patterns

### Free Courses

1. **[Redis University - RU101](https://university.redis.com/courses/ru101/)** - Introduction to Redis
2. **[Redis University - RU102PY](https://university.redis.com/courses/ru102py/)** - Redis for Python
3. **[Redis University - RU202](https://university.redis.com/courses/ru202/)** - Redis Streams
4. **[Redis University - RU301](https://university.redis.com/courses/ru301/)** - Running Redis at Scale

### Video Tutorials

- **[Redis Crash Course](https://www.youtube.com/watch?v=jgpVdJB2sKQ)** - Traversy Media (1h)
- **[Redis In-Depth](https://www.youtube.com/watch?v=Hbt56gFj998)** - Hussein Nasser (3h)
- **[Redis Microservices](https://www.youtube.com/watch?v=vfFPyG77QJc)** - Redis Labs (45m)

### Books

1. **[Redis in Action](https://www.manning.com/books/redis-in-action)** - Josiah Carlson (Manning)
2. **[The Little Redis Book](https://www.openmymind.net/redis.pdf)** - Karl Seguin (Free PDF)
3. **[Redis Essentials](https://www.packtpub.com/product/redis-essentials/9781784392451)** - Maxwell Da Silva

### Blogs & Articles

- **[Redis Blog](https://redis.com/blog/)** - Official blog
- **[Redis Weekly](https://redisweekly.com/)** - Weekly newsletter
- **[Scaling Redis at Twitter](https://blog.twitter.com/engineering/en_us/topics/infrastructure/2014/caching-with-twemcache)** - Twitter Engineering

### Interactive Learning

- **[Try Redis](https://try.redis.io/)** - Interactive tutorial in browser
- **[Redis Labs Interactive Tutorials](https://redis.com/try-free/)** - Hands-on labs

---

## 🔗 Quick Links

| Resource | Link |
|----------|------|
| 🏠 Homepage | https://redis.io |
| 📖 Documentation | https://redis.io/docs |
| 💻 GitHub | https://github.com/redis/redis |
| 🐳 Docker Hub | https://hub.docker.com/_/redis |
| 🎓 Redis University | https://university.redis.com |
| 📊 RedisInsight GUI | https://redis.com/redis-enterprise/redis-insight/ |
| 🔍 Command Reference | https://redis.io/commands |
| 💬 Discord | https://discord.gg/redis |
| 🐦 Twitter | https://twitter.com/redisinc |

---

## 🎉 Conclusion

Redis 8 brings unprecedented performance improvements and AI-ready features like **LangCache** and **vector sets**, making it the perfect choice for:

✅ **Ultra-low latency applications** (<1ms)
✅ **High-performance caching** (1M+ ops/sec)
✅ **Real-time analytics and leaderboards**
✅ **AI/ML semantic caching** (90%+ cost savings)
✅ **Session management at scale**
✅ **Distributed systems coordination**

**Next Steps:**
1. [Explore Redis + AI Agents →](REDIS-AI-AGENTS.md) (Coming next!)
2. [Compare with Kafka →](KAFKA.md)
3. [Compare with RabbitMQ →](README.md)

---

<div align="center">

**⭐ Star this repo if you found it helpful!**

[🏠 Back to Main README](README.md) | [🤖 AI Agents Guide →](REDIS-AI-AGENTS.md)

</div>
