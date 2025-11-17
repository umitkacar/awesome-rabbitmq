<div align="center">

# 🚀 Awesome Message Brokers

<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&size=32&duration=2800&pause=2000&color=F75C7E&center=true&vCenter=true&width=600&lines=RabbitMQ+%7C+Kafka+%7C+Redis;Production-Ready+Guides;AI+Agents+Integration;2025+Edition" alt="Typing SVG" />
</p>

### _The Ultimate Guide to Modern Message Brokers & Event Streaming Platforms_

<p align="center">
  <i>Comprehensive documentation covering RabbitMQ, Apache Kafka, and Redis</i><br>
  <i>with AI Agents integration, production deployment guides, and best practices</i>
</p>

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License](https://img.shields.io/badge/License-CC0_1.0-green?style=for-the-badge)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=for-the-badge)](CONTRIBUTING.md)
[![Last Updated](https://img.shields.io/badge/Updated-2025-blue?style=for-the-badge)]()

<p align="center">
  <a href="#-rabbitmq">RabbitMQ</a> •
  <a href="#-apache-kafka">Kafka</a> •
  <a href="#-redis">Redis</a> •
  <a href="#-comparison">Comparison</a> •
  <a href="#-contributing">Contributing</a>
</p>

</div>

---

## 📊 Quick Overview

<table>
<tr>
<td width="33%" valign="top">

### 🐰 RabbitMQ
**Traditional Message Broker**

```
┌─────────────────┐
│   Throughput    │
│   ~50K msg/s    │
├─────────────────┤
│    Latency      │
│     1-5ms       │
├─────────────────┤
│   Best For      │
│  Task Queues    │
│  RPC Patterns   │
└─────────────────┘
```

🎯 **Strengths:**
- ✅ Complex routing
- ✅ Message priority
- ✅ Multiple protocols
- ✅ Easy to use

[📖 Full Guide →](rabbitmq/)

</td>
<td width="33%" valign="top">

### ⚡ Apache Kafka
**Event Streaming Platform**

```
┌─────────────────┐
│   Throughput    │
│   ~1M msg/s     │
├─────────────────┤
│    Latency      │
│    5-10ms       │
├─────────────────┤
│   Best For      │
│Event Streaming  │
│ Log Aggregation │
└─────────────────┘
```

🎯 **Strengths:**
- ✅ High throughput
- ✅ Message replay
- ✅ Scalability
- ✅ Durability

[📖 Full Guide →](kafka/)

</td>
<td width="33%" valign="top">

### 💎 Redis
**In-Memory Data Store**

```
┌─────────────────┐
│   Throughput    │
│   ~1M ops/s     │
├─────────────────┤
│    Latency      │
│      <1ms       │
├─────────────────┤
│   Best For      │
│    Caching      │
│   Real-Time     │
└─────────────────┘
```

🎯 **Strengths:**
- ✅ Ultra-low latency
- ✅ Rich data types
- ✅ Pub/Sub
- ✅ Vector search

[📖 Full Guide →](redis/)

</td>
</tr>
</table>

---

## 🎨 What's Inside?

<div align="center">

| 📚 Topic | 🐰 RabbitMQ | ⚡ Kafka | 💎 Redis |
|---------|------------|---------|---------|
| **Core Documentation** | [Guide](rabbitmq/README.md) | [Guide](kafka/README.md) | [Guide](redis/README.md) |
| **AI Agents Integration** | [AI Guide](rabbitmq/AI-AGENTS.md) | [AI Guide](kafka/AI-AGENTS.md) | [AI Guide](redis/AI-AGENTS.md) |
| **Installation** | ✅ Docker, K8s, Native | ✅ Docker, K8s, KRaft | ✅ Docker, K8s, Cloud |
| **Architecture** | ✅ Deep Dive | ✅ Deep Dive | ✅ Deep Dive |
| **Client Libraries** | ✅ All Languages | ✅ All Languages | ✅ All Languages |
| **Monitoring** | ✅ Prometheus/Grafana | ✅ Prometheus/Grafana | ✅ Prometheus/Grafana |
| **Production Best Practices** | ✅ Complete | ✅ Complete | ✅ Complete |
| **Code Examples** | ✅ 30+ Examples | ✅ 30+ Examples | ✅ 30+ Examples |

</div>

---

## 🐰 RabbitMQ

<div align="center">
<img src="https://www.rabbitmq.com/img/rabbitmq-logo-with-name.svg" alt="RabbitMQ" width="300"/>
</div>

### 📋 What You'll Learn

**RabbitMQ 4.2.0** - The most popular message broker with AMQP protocol support

<details>
<summary><b>🎯 Core Topics</b></summary>

#### Main Documentation ([rabbitmq/README.md](rabbitmq/README.md))
- 🚀 **Getting Started**
  - Docker deployment with management UI
  - Kubernetes deployment with cluster operator
  - Production configuration & tuning

- 🏗️ **Architecture Deep Dive**
  - Exchanges (Direct, Topic, Fanout, Headers)
  - Queues, bindings, and routing
  - Virtual hosts and permissions
  - Clustering and high availability

- 💻 **Client Libraries**
  - Python (Pika, aio-pika)
  - Node.js (amqplib)
  - Go (amqp091-go)
  - Java (Spring AMQP)
  - Full code examples for each

- 📊 **Monitoring & Operations**
  - Prometheus exporters
  - Grafana dashboards
  - Health checks and alerts
  - Performance tuning

- 🎯 **Use Cases & Patterns**
  - Task queues and work distribution
  - Request/Reply (RPC) patterns
  - Event broadcasting
  - Priority queues

</details>

<details>
<summary><b>🤖 AI & ML Integration</b></summary>

#### AI Agents Guide ([rabbitmq/AI-AGENTS.md](rabbitmq/AI-AGENTS.md))
- 🧠 **Multi-Agent Systems**
  - Agent task distribution patterns
  - Queue-based agent coordination
  - Load balancing across agents

- 🔌 **Framework Integration**
  - LangChain with RabbitMQ
  - AutoGen agent communication
  - CrewAI task queues
  - Custom agent architectures

- 📦 **Production Examples**
  - Distributed AI processing pipeline
  - Agent result aggregation
  - Error handling and retry logic
  - Scalable agent orchestration

- 🎯 **Real-World Use Cases**
  - Document processing agents
  - Multi-step AI workflows
  - Agent-to-agent messaging
  - Production case studies

</details>

**📚 [Explore RabbitMQ Documentation →](rabbitmq/)**

---

## ⚡ Apache Kafka

<div align="center">
<img src="https://kafka.apache.org/logos/kafka-logo-wide.png" alt="Apache Kafka" width="300"/>
</div>

### 📋 What You'll Learn

**Apache Kafka 4.0** - High-throughput distributed event streaming platform

<details>
<summary><b>🎯 Core Topics</b></summary>

#### Main Documentation ([kafka/README.md](kafka/README.md))
- 🚀 **Kafka 4.0 New Features**
  - KRaft mode (ZooKeeper removal)
  - Kafka Queues for simple use cases
  - Enhanced security features
  - Performance improvements

- 🏗️ **Architecture Deep Dive**
  - Topics, partitions, and replication
  - Producers and consumers
  - Consumer groups
  - Kafka Streams API

- ☸️ **Deployment Options**
  - Docker Compose setup
  - Kubernetes with Strimzi operator
  - Helm charts for production
  - Cloud-native deployments

- 💻 **Client Libraries**
  - Python (kafka-python, confluent-kafka)
  - Node.js (kafkajs)
  - Go (kafka-go)
  - Java (official clients)

- 📊 **Monitoring & Operations**
  - JMX metrics and exporters
  - Kafka UI tools
  - Performance benchmarking
  - Production best practices

- 🎯 **Stream Processing**
  - Kafka Streams applications
  - ksqlDB for SQL queries
  - Apache Flink integration
  - Real-time analytics

</details>

<details>
<summary><b>🤖 AI & ML Integration</b></summary>

#### AI Agents Guide ([kafka/AI-AGENTS.md](kafka/AI-AGENTS.md))
- 🧠 **Event-Driven AI Agents**
  - Event streaming for agent coordination
  - Multi-agent orchestration patterns
  - Message replay for agent training

- 🔌 **Advanced Integration**
  - MCP (Model Context Protocol) over Kafka
  - A2A (Agent2Agent Protocol)
  - Apache Flink + LLM orchestration
  - Real-time ML inference with Kafka Streams

- 🗄️ **Vector Database Integration**
  - Kafka → Pinecone pipeline
  - Weaviate streaming ingestion
  - Real-time embedding generation
  - Semantic search systems

- 🏢 **Production Case Studies**
  - LinkedIn AI infrastructure
  - Uber real-time ML
  - ING Bank fraud detection
  - Large-scale deployments

</details>

**📚 [Explore Kafka Documentation →](kafka/)**

---

## 💎 Redis

<div align="center">
<img src="https://redis.io/images/redis-white.png" alt="Redis" width="300" style="background: #DC382D; padding: 20px; border-radius: 10px;"/>
</div>

### 📋 What You'll Learn

**Redis 8.0** - Ultra-fast in-memory data store with AI capabilities

<details>
<summary><b>🎯 Core Topics</b></summary>

#### Main Documentation ([redis/README.md](redis/README.md))
- 🚀 **Redis 8 New Features**
  - LangCache for semantic caching (70-90% cost savings!)
  - Vector Sets - new data type for AI
  - Redis Flex - hybrid RAM/SSD storage
  - 87% faster commands, 2x throughput

- 🏗️ **Architecture & Data Structures**
  - 15+ data structures (Strings, Hashes, Lists, Sets, etc.)
  - Persistence options (RDB + AOF)
  - Clustering and replication
  - Memory optimization

- ☸️ **Deployment Options**
  - Docker deployment
  - Kubernetes with Redis Enterprise Operator
  - Redis Cloud
  - Production configuration

- 💻 **Client Libraries**
  - Python (redis-py, redis-om)
  - Node.js (node-redis)
  - Go (go-redis)
  - Java (Jedis, Lettuce)

- 📊 **Performance Optimization**
  - <1ms latency techniques
  - Connection pooling
  - Pipelining
  - Memory management

- 🎯 **Use Cases & Patterns**
  - Caching strategies
  - Session management
  - Rate limiting
  - Leaderboards
  - Real-time analytics

</details>

<details>
<summary><b>🤖 AI & ML Integration</b></summary>

#### AI Agents Guide ([redis/AI-AGENTS.md](redis/AI-AGENTS.md))
- 🧠 **Redis as AI Agent Memory** (#1 choice - 43% adoption!)
  - Short-term memory (conversation context)
  - Long-term memory (vector embeddings)
  - Structured memory (user profiles)

- 💰 **LangCache - Semantic Caching**
  - 70-90% LLM cost reduction
  - Semantic similarity matching
  - Production-ready examples
  - ROI calculator included

- 🔍 **RedisVL - Vector Database**
  - Sub-millisecond vector search
  - RAG (Retrieval-Augmented Generation)
  - Similarity search for embeddings
  - Integration with OpenAI, Cohere

- 🔌 **Framework Integration**
  - LangChain RedisVectorStore
  - LangGraph checkpointing
  - AutoGen Redis caching
  - CrewAI state management

- 🏢 **Production Case Studies**
  - Raymond James financial chatbot
  - Amgen scientific document analysis
  - Real-world AI deployments
  - Performance benchmarks

</details>

**📚 [Explore Redis Documentation →](redis/)**

---

## 📊 Comparison

### When Should You Use Each?

<table>
<tr>
<th width="25%">Scenario</th>
<th width="25%">🐰 RabbitMQ</th>
<th width="25%">⚡ Kafka</th>
<th width="25%">💎 Redis</th>
</tr>

<tr>
<td><b>Task Queues</b></td>
<td>✅ <b>Best Choice</b><br>Built for this</td>
<td>⚠️ Overkill<br>Too complex</td>
<td>✅ Simple queues<br>Lists work well</td>
</tr>

<tr>
<td><b>Event Streaming</b></td>
<td>❌ Not designed<br>for this</td>
<td>✅ <b>Best Choice</b><br>Purpose-built</td>
<td>⚠️ Pub/Sub only<br>No replay</td>
</tr>

<tr>
<td><b>Caching</b></td>
<td>❌ Wrong tool</td>
<td>❌ Wrong tool</td>
<td>✅ <b>Best Choice</b><br>Ultra-fast</td>
</tr>

<tr>
<td><b>Message Replay</b></td>
<td>❌ Limited support</td>
<td>✅ <b>Best Choice</b><br>Full replay</td>
<td>❌ Not supported</td>
</tr>

<tr>
<td><b>Real-Time AI</b></td>
<td>✅ Agent queues<br>Good for tasks</td>
<td>✅ Event-driven<br>Stream processing</td>
<td>✅ <b>Best Choice</b><br>Agent memory</td>
</tr>

<tr>
<td><b>Microservices</b></td>
<td>✅ <b>Excellent</b><br>Service-to-service</td>
<td>✅ <b>Excellent</b><br>Event-driven</td>
<td>✅ Good<br>Cache + Pub/Sub</td>
</tr>

<tr>
<td><b>High Throughput</b></td>
<td>⚠️ ~50K msg/s<br>Limited</td>
<td>✅ <b>Best Choice</b><br>1M+ msg/s</td>
<td>✅ <b>Excellent</b><br>1M+ ops/s</td>
</tr>

<tr>
<td><b>Low Latency</b></td>
<td>✅ 1-5ms<br>Very good</td>
<td>⚠️ 5-10ms<br>Good</td>
<td>✅ <b>Best Choice</b><br>&lt;1ms</td>
</tr>

</table>

### 🎯 Decision Tree

```
Start Here
    │
    ├─ Need ultra-low latency (<1ms)?
    │   └─ YES → 💎 Redis
    │
    ├─ Need to replay messages?
    │   └─ YES → ⚡ Kafka
    │
    ├─ Need complex routing?
    │   └─ YES → 🐰 RabbitMQ
    │
    ├─ Event streaming / Log aggregation?
    │   └─ YES → ⚡ Kafka
    │
    ├─ Traditional task queues?
    │   └─ YES → 🐰 RabbitMQ
    │
    ├─ Caching layer?
    │   └─ YES → 💎 Redis
    │
    └─ AI Agent memory?
        └─ YES → 💎 Redis (43% adoption!)
```

---

## 🎯 Use Case Matrix

<div align="center">

| Use Case | 🐰 RabbitMQ | ⚡ Kafka | 💎 Redis | Best Choice |
|----------|------------|---------|---------|-------------|
| **Async Task Processing** | ✅✅✅ | ✅ | ✅ | 🐰 RabbitMQ |
| **Event Sourcing** | ❌ | ✅✅✅ | ❌ | ⚡ Kafka |
| **Caching** | ❌ | ❌ | ✅✅✅ | 💎 Redis |
| **Log Aggregation** | ⚠️ | ✅✅✅ | ❌ | ⚡ Kafka |
| **RPC / Request-Reply** | ✅✅✅ | ❌ | ✅ | 🐰 RabbitMQ |
| **Real-Time Analytics** | ❌ | ✅✅✅ | ✅✅ | ⚡ Kafka |
| **Session Management** | ❌ | ❌ | ✅✅✅ | 💎 Redis |
| **AI Agent Memory** | ✅ | ✅ | ✅✅✅ | 💎 Redis |
| **Message Priority** | ✅✅✅ | ❌ | ✅ | 🐰 RabbitMQ |
| **Pub/Sub Messaging** | ✅✅ | ✅✅✅ | ✅✅ | ⚡ Kafka |
| **Microservices Communication** | ✅✅✅ | ✅✅✅ | ✅✅ | Both! |

**Legend:** ✅✅✅ Excellent | ✅✅ Good | ✅ Acceptable | ⚠️ Limited | ❌ Not Suitable

</div>

---

## 🚀 Quick Start

### Installation Commands

<table>
<tr>
<td width="33%">

#### 🐰 RabbitMQ

```bash
# Docker
docker run -d \
  --name rabbitmq \
  -p 5672:5672 \
  -p 15672:15672 \
  rabbitmq:4.2-management

# UI: http://localhost:15672
# User: guest / guest
```

[Full Setup →](rabbitmq/README.md#-getting-started)

</td>
<td width="33%">

#### ⚡ Kafka

```bash
# Docker Compose
curl -O https://raw.githubusercontent.com/\
apache/kafka/trunk/docker/examples/\
jvm/single-node/plaintext/\
docker-compose.yml

docker-compose up -d
```

[Full Setup →](kafka/README.md#-getting-started)

</td>
<td width="33%">

#### 💎 Redis

```bash
# Docker
docker run -d \
  --name redis \
  -p 6379:6379 \
  redis:8-alpine

# Test
redis-cli ping
# PONG
```

[Full Setup →](redis/README.md#-getting-started)

</td>
</tr>
</table>

---

## 📚 Documentation Structure

```
awesome-message-brokers/
│
├── 📄 README.md (You are here!)
│
├── 🐰 rabbitmq/
│   ├── README.md              # Complete RabbitMQ guide
│   └── AI-AGENTS.md           # AI agents integration
│
├── ⚡ kafka/
│   ├── README.md              # Complete Kafka guide
│   └── AI-AGENTS.md           # AI agents integration
│
├── 💎 redis/
│   ├── README.md              # Complete Redis guide
│   └── AI-AGENTS.md           # AI agents integration
│
├── 🤝 CONTRIBUTING.md         # Contribution guidelines
└── 📜 LICENSE                 # CC0 1.0 Universal
```

---

## 🎓 Learning Path

### Beginner Level
1. Start with **RabbitMQ** - easiest to understand
   - Read [rabbitmq/README.md](rabbitmq/README.md)
   - Deploy with Docker
   - Try the examples

2. Learn **Redis** basics
   - Read [redis/README.md](redis/README.md)
   - Practice with data structures
   - Implement caching patterns

3. Explore **Kafka** fundamentals
   - Read [kafka/README.md](kafka/README.md)
   - Understand topics and partitions
   - Try producer/consumer examples

### Intermediate Level
- Dive into architecture details in each guide
- Set up monitoring with Prometheus/Grafana
- Deploy on Kubernetes
- Implement production patterns

### Advanced Level
- Explore AI agents integration in all three
- Build multi-technology systems
- Optimize for production workloads
- Contribute back to this repo!

---

## 🤖 AI & ML Integration

All three technologies have comprehensive AI agent integration guides:

<table>
<tr>
<th width="33%">🐰 RabbitMQ</th>
<th width="33%">⚡ Kafka</th>
<th width="33%">💎 Redis</th>
</tr>

<tr>
<td valign="top">

**Agent Task Distribution**
- Queue-based coordination
- Load balancing
- Priority handling

**Frameworks:**
- LangChain
- AutoGen
- CrewAI

[AI Guide →](rabbitmq/AI-AGENTS.md)

</td>
<td valign="top">

**Event-Driven Agents**
- Stream processing
- Message replay
- Real-time ML

**Advanced:**
- MCP/A2A protocols
- Apache Flink + LLM
- Vector DB integration

[AI Guide →](kafka/AI-AGENTS.md)

</td>
<td valign="top">

**Agent Memory (#1)**
- 43% adoption rate
- 3 memory types
- <1ms latency

**Cost Savings:**
- LangCache: 70-90%
- Semantic caching
- Vector search

[AI Guide →](redis/AI-AGENTS.md)

</td>
</tr>
</table>

---

## 📊 Statistics & Metrics

<div align="center">

### Repository Stats

![Lines of Documentation](https://img.shields.io/badge/Lines%20of%20Docs-6000%2B-brightgreen?style=for-the-badge)
![Code Examples](https://img.shields.io/badge/Code%20Examples-90%2B-blue?style=for-the-badge)
![Technologies Covered](https://img.shields.io/badge/Technologies-3-orange?style=for-the-badge)
![Frameworks](https://img.shields.io/badge/Frameworks-15%2B-purple?style=for-the-badge)

### Coverage Breakdown

| Metric | Count |
|--------|-------|
| 📄 Total Documentation Lines | 6,000+ |
| 💻 Production Code Examples | 90+ |
| 🔍 Web Searches Conducted | 60 (20 per tech) |
| 🎯 Technologies Covered | 3 major platforms |
| 🤖 AI Frameworks Integrated | 10+ frameworks |
| 🌍 Languages | Python, JS, Go, Java |
| ☸️ Deployment Options | Docker, K8s, Cloud |
| 📊 Monitoring Tools | Prometheus, Grafana |

</div>

---

## 🌟 Key Features

### ✨ What Makes This Repo Special?

- 🎯 **Comprehensive Coverage** - 6,000+ lines of production-ready documentation
- 🤖 **AI-First Approach** - Dedicated AI agents integration for all three technologies
- 💻 **Code-Heavy** - 90+ working examples in multiple languages
- 🔬 **Research-Backed** - 60 parallel web searches conducted (20 per technology)
- 🚀 **Production-Ready** - Real deployment guides, monitoring, and best practices
- 📊 **Modern Tools** - Kubernetes, Prometheus, Grafana, Docker
- 🎓 **Educational** - Clear explanations, diagrams, and learning paths
- 🆕 **Up-to-Date** - Covers latest versions (RabbitMQ 4.2, Kafka 4.0, Redis 8.0)

---

## 🤝 Contributing

We welcome contributions! This repository is maintained with high quality standards.

### How to Contribute

1. **Fork the repository**
2. **Create a feature branch** (`git checkout -b feature/amazing-feature`)
3. **Make your changes** (follow our documentation style)
4. **Commit your changes** (`git commit -m 'Add amazing feature'`)
5. **Push to the branch** (`git push origin feature/amazing-feature`)
6. **Open a Pull Request**

### Contribution Guidelines

- ✅ Maintain the existing documentation style
- ✅ Include code examples for technical concepts
- ✅ Add links to official documentation
- ✅ Test all code examples before submitting
- ✅ Update the relevant comparison tables
- ✅ Follow markdown best practices

See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed guidelines.

---

## 📜 License

This work is licensed under [CC0 1.0 Universal](LICENSE) - feel free to use, modify, and share!

### What This Means

- ✅ **Commercial use** - Use in commercial projects
- ✅ **Modification** - Adapt and build upon
- ✅ **Distribution** - Share freely
- ✅ **Private use** - Use privately
- ❌ **No attribution required** - But appreciated!

---

## 🙏 Acknowledgments

This repository was created with extensive research across:

- 📚 Official documentation for RabbitMQ, Kafka, and Redis
- 🌐 60 parallel web searches across multiple sources
- 🤖 AI/ML community best practices
- 🏢 Production case studies from industry leaders
- 👥 Open-source community contributions

Special thanks to the maintainers and communities of:
- [RabbitMQ](https://www.rabbitmq.com/)
- [Apache Kafka](https://kafka.apache.org/)
- [Redis](https://redis.io/)
- [LangChain](https://www.langchain.com/)
- [LangGraph](https://www.langchain.com/langgraph)
- All the amazing open-source projects mentioned in this repo

---

## 📞 Support & Community

- 💬 **Discussions** - [GitHub Discussions](../../discussions)
- 🐛 **Issues** - [Report bugs or request features](../../issues)
- ⭐ **Star this repo** - If you find it helpful!
- 🔄 **Share** - Help others discover this resource

---

## 🔗 Quick Links

<div align="center">

### 🐰 RabbitMQ
[![Docs](https://img.shields.io/badge/📖%20Docs-Read%20Now-orange?style=for-the-badge)](rabbitmq/README.md)
[![AI Guide](https://img.shields.io/badge/🤖%20AI%20Guide-Explore-orange?style=for-the-badge)](rabbitmq/AI-AGENTS.md)
[![Official](https://img.shields.io/badge/🌐%20Official-Visit-orange?style=for-the-badge)](https://www.rabbitmq.com/)

### ⚡ Apache Kafka
[![Docs](https://img.shields.io/badge/📖%20Docs-Read%20Now-black?style=for-the-badge)](kafka/README.md)
[![AI Guide](https://img.shields.io/badge/🤖%20AI%20Guide-Explore-black?style=for-the-badge)](kafka/AI-AGENTS.md)
[![Official](https://img.shields.io/badge/🌐%20Official-Visit-black?style=for-the-badge)](https://kafka.apache.org/)

### 💎 Redis
[![Docs](https://img.shields.io/badge/📖%20Docs-Read%20Now-red?style=for-the-badge)](redis/README.md)
[![AI Guide](https://img.shields.io/badge/🤖%20AI%20Guide-Explore-red?style=for-the-badge)](redis/AI-AGENTS.md)
[![Official](https://img.shields.io/badge/🌐%20Official-Visit-red?style=for-the-badge)](https://redis.io/)

</div>

---

<div align="center">

## ⭐ Star History

[![Star History Chart](https://api.star-history.com/svg?repos=umitkacar/awesome-rabbitmq&type=Date)](https://star-history.com/#umitkacar/awesome-rabbitmq&Date)

---

### Made with ❤️ by the community

**Last Updated:** November 2025 | **Version:** 2.0.0

<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&pause=1000&color=F75C7E&center=true&vCenter=true&width=435&lines=Happy+Messaging!;Build+Awesome+Systems!;Scale+with+Confidence!" alt="Typing SVG" />
</p>

[⬆ Back to Top](#-awesome-message-brokers)

</div>
