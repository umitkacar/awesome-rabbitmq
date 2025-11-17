<div align="center">

# 🐰 Awesome RabbitMQ [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

<img src="https://www.rabbitmq.com/img/rabbitmq-logo-with-name.svg" alt="RabbitMQ Logo" width="400"/>

### _The most comprehensive, curated list of RabbitMQ resources, tools, and best practices_

[![RabbitMQ Version](https://img.shields.io/badge/RabbitMQ-4.2.0-orange?style=for-the-badge&logo=rabbitmq)](https://www.rabbitmq.com/)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=for-the-badge)](http://makeapullrequest.com)
[![Last Updated](https://img.shields.io/badge/Updated-2025-blue?style=for-the-badge)](https://github.com)

<p align="center">
  <a href="#-what-is-rabbitmq">What is RabbitMQ?</a> •
  <a href="#-getting-started">Getting Started</a> •
  <a href="#-ai--ml-integration">AI & ML</a> •
  <a href="#-official-resources">Resources</a> •
  <a href="#-tools--plugins">Tools</a> •
  <a href="#-contributing">Contributing</a>
</p>

</div>

---

## 📋 Table of Contents

- [🎯 What is RabbitMQ?](#-what-is-rabbitmq)
- [🚀 Getting Started](#-getting-started)
  - [💻 Installation](#-installation)
  - [🐳 Docker Deployment](#-docker-deployment)
  - [☸️ Kubernetes Deployment](#️-kubernetes-deployment)
  - [⚙️ Configuration & Setup](#️-configuration--setup)
- [🤖 AI & ML Integration](#-ai--ml-integration)
- [🏗️ Architecture & Design Patterns](#️-architecture--design-patterns)
- [📚 Client Libraries & SDKs](#-client-libraries--sdks)
- [🔧 Tools & Plugins](#-tools--plugins)
- [📊 Monitoring & Observability](#-monitoring--observability)
- [📖 Learning Resources](#-learning-resources)
- [🎓 Tutorials & Courses](#-tutorials--courses)
- [⚡ Performance & Optimization](#-performance--optimization)
- [🔒 Security Best Practices](#-security-best-practices)
- [🆚 Comparisons](#-comparisons)
- [🌟 Awesome Projects](#-awesome-projects)
- [🤝 Contributing](#-contributing)
- [📜 License](#-license)

---

## 🎯 What is RabbitMQ?

<details open>
<summary><b>Click to expand/collapse</b></summary>

**RabbitMQ** is a robust, feature-rich, open-source message broker that implements the Advanced Message Queuing Protocol (AMQP). It enables applications to communicate asynchronously by passing messages through queues, making it ideal for building scalable, distributed systems.

### 🌟 Key Features

- **🔄 Multiple Messaging Protocols**: AMQP 0.9.1, AMQP 1.0, MQTT, STOMP
- **📬 Flexible Routing**: Direct, Topic, Fanout, and Headers exchanges
- **🔒 Reliability**: Message acknowledgments, persistence, and delivery guarantees
- **🌐 Clustering**: High availability through node clustering
- **📊 Management UI**: Built-in web-based monitoring and management
- **🔌 Plugin System**: Extensible architecture with rich plugin ecosystem
- **💾 Streams**: Modern streaming capabilities for high-throughput scenarios
- **🎯 Priority Queues**: Message prioritization support
- **⏰ Dead Letter Exchanges**: Handle failed message processing gracefully

### ✅ Advantages

| Feature | Benefit |
|---------|---------|
| 🎯 **Mature & Proven** | Battle-tested in production for over 15 years |
| 🔧 **Easy to Use** | Simple to set up and integrate with minimal configuration |
| 📝 **Standards-Based** | Full AMQP compliance ensures interoperability |
| 🌍 **Multi-Language Support** | Client libraries for virtually every programming language |
| 🔄 **Flexible Routing** | Powerful exchange types for complex message routing |
| 📊 **Management Tools** | Excellent built-in monitoring and management interfaces |
| 🔌 **Plugin Ecosystem** | Rich ecosystem of plugins for extended functionality |
| 🛡️ **Reliability** | Strong message delivery guarantees and persistence options |
| 📖 **Documentation** | Comprehensive, well-maintained documentation |
| 👥 **Community** | Large, active community and commercial support available |

### ⚠️ Trade-offs

| Consideration | Details |
|---------------|---------|
| ⚡ **Throughput** | Lower raw throughput compared to Kafka (~50K vs 1M msgs/sec) |
| 💾 **Message Retention** | Not designed for long-term message storage or replay |
| 📈 **Scalability** | Vertical scaling preferred; horizontal scaling has limitations |
| 🔧 **Complexity** | Can become complex with many queues and exchanges |
| 💻 **Memory Usage** | Higher memory consumption for message buffering |
| 🔄 **Message Ordering** | Strict ordering only guaranteed within single queue |

### 🎯 Best Use Cases

- ✅ Traditional message queue patterns (task distribution, work queues)
- ✅ Event-driven microservices architectures
- ✅ Request/reply patterns with RPC
- ✅ Complex routing requirements
- ✅ Priority-based message processing
- ✅ When you need strong delivery guarantees
- ✅ Integration with legacy systems using AMQP

### ❌ When NOT to Use RabbitMQ

- ❌ High-throughput streaming (millions of events/second) → Use Kafka
- ❌ Long-term event storage and replay → Use Kafka or event sourcing DB
- ❌ Simple pub/sub with minimal latency → Use Redis Pub/Sub
- ❌ Real-time analytics on streaming data → Use Kafka or Pulsar
- ❌ Extremely low latency requirements (<1ms) → Use Redis

### 🆕 What's New in RabbitMQ 4.2.0 (2025)

- 🎯 **Message Interceptors**: Intercept incoming/outgoing messages across protocols
- 🔍 **SQL Filter Expressions**: Server-side filtering for streams (4M+ msgs/sec)
- 🔄 **Blue-Green Deployment**: Improved migration tools with rabbitmqadmin v2
- 🚀 **AMQP 1.0 Enhancements**: JMS temporary queues and dynamic queues support
- 💾 **Khepri Metadata Store**: Alternative to Mnesia for metadata storage
- ⚡ **Performance Optimizations**: Dramatic improvements for low-throughput streams

</details>

---

## 🚀 Getting Started

### 💻 Installation

<details>
<summary><b>Click to expand installation methods</b></summary>

#### 🐧 Linux (Ubuntu/Debian)

```bash
# Add RabbitMQ signing key
curl -fsSL https://packagecloud.io/rabbitmq/rabbitmq-server/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/rabbitmq.gpg

# Add repository
sudo tee /etc/apt/sources.list.d/rabbitmq.list <<EOF
deb [signed-by=/usr/share/keyrings/rabbitmq.gpg] https://packagecloud.io/rabbitmq/rabbitmq-server/ubuntu/ focal main
EOF

# Update and install
sudo apt-get update
sudo apt-get install rabbitmq-server -y

# Start and enable service
sudo systemctl start rabbitmq-server
sudo systemctl enable rabbitmq-server
```

#### 🍎 macOS

```bash
# Using Homebrew
brew update
brew install rabbitmq

# Start RabbitMQ
brew services start rabbitmq
```

#### 🪟 Windows

Download the installer from [rabbitmq.com/download](https://www.rabbitmq.com/download.html) or use Chocolatey:

```powershell
choco install rabbitmq
```

#### 📦 From Source

```bash
git clone https://github.com/rabbitmq/rabbitmq-server.git
cd rabbitmq-server
make
make run
```

</details>

### 🐳 Docker Deployment

<details>
<summary><b>Click to expand Docker deployment options</b></summary>

#### 🎯 Quick Start

```bash
# Run RabbitMQ with management plugin
docker run -d \
  --name rabbitmq \
  -p 5672:5672 \
  -p 15672:15672 \
  -e RABBITMQ_DEFAULT_USER=admin \
  -e RABBITMQ_DEFAULT_PASS=admin \
  rabbitmq:4.2-management
```

#### 🔧 Production-Ready Configuration

```yaml
# docker-compose.yml
version: '3.8'

services:
  rabbitmq:
    image: rabbitmq:4.2-management-alpine
    container_name: rabbitmq
    hostname: rabbitmq
    restart: unless-stopped

    environment:
      RABBITMQ_DEFAULT_USER: ${RABBITMQ_USER:-admin}
      RABBITMQ_DEFAULT_PASS: ${RABBITMQ_PASSWORD:-secure_password}
      RABBITMQ_DEFAULT_VHOST: ${RABBITMQ_VHOST:-/}
      RABBITMQ_ERLANG_COOKIE: ${RABBITMQ_ERLANG_COOKIE:-secret_cookie}

    ports:
      - "5672:5672"    # AMQP
      - "15672:15672"  # Management UI
      - "15692:15692"  # Prometheus metrics

    volumes:
      - rabbitmq_data:/var/lib/rabbitmq
      - rabbitmq_logs:/var/log/rabbitmq
      - ./rabbitmq.conf:/etc/rabbitmq/rabbitmq.conf:ro

    healthcheck:
      test: ["CMD", "rabbitmq-diagnostics", "ping"]
      interval: 30s
      timeout: 10s
      retries: 5

    networks:
      - rabbitmq_network

  prometheus:
    image: prom/prometheus:latest
    ports:
      - "9090:9090"
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml
    networks:
      - rabbitmq_network

  grafana:
    image: grafana/grafana:latest
    ports:
      - "3000:3000"
    environment:
      GF_SECURITY_ADMIN_PASSWORD: admin
    volumes:
      - grafana_data:/var/lib/grafana
    networks:
      - rabbitmq_network

volumes:
  rabbitmq_data:
  rabbitmq_logs:
  grafana_data:

networks:
  rabbitmq_network:
    driver: bridge
```

#### 📝 Sample rabbitmq.conf

```ini
# Network & Protocol
listeners.tcp.default = 5672
management.tcp.port = 15672
prometheus.tcp.port = 15692

# Memory & Disk
vm_memory_high_watermark.relative = 0.6
disk_free_limit.absolute = 2GB

# Clustering
cluster_formation.peer_discovery_backend = rabbit_peer_discovery_classic_config
cluster_partition_handling = autoheal

# Logging
log.console = true
log.console.level = info
log.file = false

# Performance
channel_max = 2048
heartbeat = 60
```

</details>

### ☸️ Kubernetes Deployment

<details>
<summary><b>Click to expand Kubernetes deployment options</b></summary>

#### 🎯 Using RabbitMQ Cluster Operator (Recommended)

```bash
# Install the operator
kubectl apply -f "https://github.com/rabbitmq/cluster-operator/releases/latest/download/cluster-operator.yml"

# Verify installation
kubectl get customresourcedefinitions.apiextensions.k8s.io
```

#### 📋 Deploy RabbitMQ Cluster

```yaml
# rabbitmq-cluster.yaml
apiVersion: rabbitmq.com/v1beta1
kind: RabbitmqCluster
metadata:
  name: production-rabbitmq
  namespace: messaging
spec:
  replicas: 3

  image: rabbitmq:4.2-management

  resources:
    requests:
      cpu: 500m
      memory: 2Gi
    limits:
      cpu: 2000m
      memory: 4Gi

  rabbitmq:
    additionalConfig: |
      cluster_partition_handling = pause_minority
      vm_memory_high_watermark_paging_ratio = 0.85
      disk_free_limit.absolute = 2GB
      collect_statistics_interval = 10000

  persistence:
    storageClassName: fast-ssd
    storage: 20Gi

  affinity:
    podAntiAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
      - labelSelector:
          matchExpressions:
          - key: app.kubernetes.io/name
            operator: In
            values:
            - production-rabbitmq
        topologyKey: kubernetes.io/hostname

  override:
    statefulSet:
      spec:
        template:
          spec:
            containers:
            - name: rabbitmq
              env:
              - name: RABBITMQ_DEFAULT_USER
                valueFrom:
                  secretKeyRef:
                    name: rabbitmq-admin
                    key: username
              - name: RABBITMQ_DEFAULT_PASS
                valueFrom:
                  secretKeyRef:
                    name: rabbitmq-admin
                    key: password
```

#### 🔐 Create Admin Secret

```bash
kubectl create secret generic rabbitmq-admin \
  --from-literal=username=admin \
  --from-literal=password=$(openssl rand -base64 32) \
  -n messaging
```

#### 🛠️ Using Helm

```bash
# Add Bitnami repository
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update

# Install RabbitMQ
helm install my-rabbitmq bitnami/rabbitmq \
  --set auth.username=admin \
  --set auth.password=secure-password \
  --set replicaCount=3 \
  --set persistence.enabled=true \
  --set persistence.size=20Gi \
  --set metrics.enabled=true \
  --set metrics.serviceMonitor.enabled=true
```

#### 📊 Best Practices for K8s Deployment

- ✅ Use **StatefulSets** for persistent identity and storage
- ✅ Enable **Pod Anti-Affinity** to distribute nodes across availability zones
- ✅ Configure **Readiness & Liveness Probes** appropriately
- ✅ Use **Persistent Volumes** with fast SSD storage
- ✅ Set **Resource Limits** to prevent resource starvation
- ✅ Enable **Prometheus Metrics** for monitoring
- ✅ Use **Secrets** for credentials management
- ✅ Configure **Network Policies** for security
- ✅ Implement **Backup Strategy** for persistence data
- ✅ Use **dedicated namespace** for isolation

</details>

### ⚙️ Configuration & Setup

<details>
<summary><b>Click to expand configuration examples</b></summary>

#### 🔧 Enable Management Plugin

```bash
rabbitmq-plugins enable rabbitmq_management
rabbitmq-plugins enable rabbitmq_prometheus
```

#### 👤 Create Users & Permissions

```bash
# Create admin user
rabbitmqctl add_user admin StrongPassword123

# Set administrator tag
rabbitmqctl set_user_tags admin administrator

# Grant permissions
rabbitmqctl set_permissions -p / admin ".*" ".*" ".*"

# Create application user
rabbitmqctl add_user app_user AppPassword456
rabbitmqctl set_permissions -p / app_user ".*" ".*" ".*"
```

#### 🏠 Virtual Hosts

```bash
# Create virtual host
rabbitmqctl add_vhost production

# Set permissions for user
rabbitmqctl set_permissions -p production admin ".*" ".*" ".*"
```

#### 📜 Policies

```bash
# HA Policy - mirror queues across all nodes
rabbitmqctl set_policy ha-all ".*" '{"ha-mode":"all","ha-sync-mode":"automatic"}' --apply-to queues

# TTL Policy - message TTL of 1 hour
rabbitmqctl set_policy ttl-policy "ttl\\..*" '{"message-ttl":3600000}' --apply-to queues

# Max Length Policy - limit queue to 10000 messages
rabbitmqctl set_policy max-length "limited\\..*" '{"max-length":10000}' --apply-to queues
```

</details>

---

## 🤖 AI & ML Integration

<div align="center">

### _Leveraging RabbitMQ for Scalable AI/ML Workloads_

</div>

<details open>
<summary><b>🎯 Why RabbitMQ for AI/ML?</b></summary>

AI/ML workloads are inherently **resource-intensive** and **time-consuming**, making asynchronous processing essential for production systems. RabbitMQ provides the perfect foundation for:

- 🔄 **Decoupling** model inference from application logic
- 📊 **Load balancing** requests across multiple GPU workers
- ⚡ **Scaling** inference services independently
- 🎯 **Prioritizing** high-value predictions
- 🔁 **Retry logic** for failed inferences
- 📈 **Monitoring** ML pipeline performance

</details>

### 🏗️ Architecture Patterns

<details>
<summary><b>1. 🎨 AI Model Deployment Pattern</b></summary>

**Use Case**: Deploy AI models as microservices with RabbitMQ handling request queuing and load balancing.

```
┌─────────────┐      ┌──────────────┐      ┌─────────────┐
│  API Server │─────▶│   RabbitMQ   │─────▶│ ML Worker 1 │
└─────────────┘      │   Exchange   │      └─────────────┘
                     │   (Fanout)   │      ┌─────────────┐
                     └──────────────┘─────▶│ ML Worker 2 │
                                            └─────────────┘
                                            ┌─────────────┐
                                           ▶│ ML Worker N │
                                            └─────────────┘
```

**Benefits**:
- ⚡ Workers can process at their own pace (1s to 5min per inference)
- 🔄 Automatic load distribution across GPU instances
- 📊 Easy horizontal scaling based on queue depth
- 🛡️ Fault tolerance with message acknowledgments

</details>

<details>
<summary><b>2. 🎬 Computer Vision Processing Pipeline</b></summary>

**Use Case**: Process video frames through multiple AI models in parallel for object detection, classification, and tracking.

```python
# Producer: Video Frame Processor
import pika
import cv2
import json
import base64

connection = pika.BlockingConnection(pika.ConnectionParameters('localhost'))
channel = connection.channel()

# Declare fanout exchange for parallel processing
channel.exchange_declare(exchange='video_frames', exchange_type='fanout')

# Read video and publish frames
cap = cv2.VideoCapture('input_video.mp4')
while cap.isOpened():
    ret, frame = cap.read()
    if not ret:
        break

    # Encode frame to base64
    _, buffer = cv2.imencode('.jpg', frame)
    frame_base64 = base64.b64encode(buffer).decode('utf-8')

    message = json.dumps({
        'frame_id': cap.get(cv2.CAP_PROP_POS_FRAMES),
        'timestamp': cap.get(cv2.CAP_PROP_POS_MSEC),
        'frame_data': frame_base64
    })

    channel.basic_publish(
        exchange='video_frames',
        routing_key='',
        body=message,
        properties=pika.BasicProperties(delivery_mode=2)  # persistent
    )

cap.release()
connection.close()
```

```python
# Consumer: Object Detection Worker
import pika
import json
import base64
import numpy as np
import cv2
from ultralytics import YOLO

# Load YOLO model
model = YOLO('yolov8n.pt')

connection = pika.BlockingConnection(pika.ConnectionParameters('localhost'))
channel = connection.channel()

# Declare queue for object detection
channel.queue_declare(queue='object_detection', durable=True)
channel.queue_bind(exchange='video_frames', queue='object_detection')

# Declare results exchange
channel.exchange_declare(exchange='detection_results', exchange_type='direct')

def callback(ch, method, properties, body):
    data = json.loads(body)

    # Decode frame
    frame_data = base64.b64decode(data['frame_data'])
    nparr = np.frombuffer(frame_data, np.uint8)
    frame = cv2.imdecode(nparr, cv2.IMREAD_COLOR)

    # Run inference
    results = model(frame)

    # Publish results
    result_message = json.dumps({
        'frame_id': data['frame_id'],
        'timestamp': data['timestamp'],
        'detections': results[0].boxes.data.tolist(),
        'model': 'yolov8n'
    })

    ch.basic_publish(
        exchange='detection_results',
        routing_key='aggregator',
        body=result_message
    )

    # Acknowledge message
    ch.basic_ack(delivery_tag=method.delivery_tag)

channel.basic_qos(prefetch_count=1)  # Process one frame at a time
channel.basic_consume(queue='object_detection', on_message_callback=callback)

print('🎬 Object Detection Worker started...')
channel.start_consuming()
```

</details>

<details>
<summary><b>3. 🧠 Scalable ML Pipeline with RedisAI</b></summary>

**Architecture**: Combine RabbitMQ for message orchestration with RedisAI for fast model inference.

```yaml
# docker-compose.yml for ML Pipeline
version: '3.8'

services:
  rabbitmq:
    image: rabbitmq:4.2-management
    ports:
      - "5672:5672"
      - "15672:15672"
    environment:
      RABBITMQ_DEFAULT_USER: ml_user
      RABBITMQ_DEFAULT_PASS: ml_pass

  redisai:
    image: redislabs/redisai:latest
    ports:
      - "6379:6379"
    volumes:
      - ./models:/models

  ml_worker:
    build: ./ml_worker
    depends_on:
      - rabbitmq
      - redisai
    environment:
      RABBITMQ_URL: amqp://ml_user:ml_pass@rabbitmq:5672
      REDIS_URL: redis://redisai:6379
    deploy:
      replicas: 3
```

```python
# ML Worker with RedisAI
import pika
import redis
import json
import numpy as np
from redisai import Client, Tensor, DType

# Connect to RabbitMQ and RedisAI
rabbitmq = pika.BlockingConnection(pika.ConnectionParameters('rabbitmq'))
channel = rabbitmq.channel()
rai = Client(host='redisai', port=6379)

# Load model into RedisAI
with open('/models/sentiment_model.onnx', 'rb') as f:
    model = f.read()
    rai.modelstore('sentiment_model', 'onnx', 'cpu', model)

def process_prediction(ch, method, properties, body):
    data = json.loads(body)

    # Prepare input tensor
    input_data = np.array(data['features'], dtype=np.float32)
    tensor = Tensor.from_numpy(input_data)

    # Run inference in RedisAI
    rai.tensorset('input', tensor)
    rai.modelexecute('sentiment_model', ['input'], ['output'])
    output_tensor = rai.tensorget('output')

    # Get prediction
    prediction = output_tensor.to_numpy()

    # Publish result
    result = json.dumps({
        'request_id': data['request_id'],
        'prediction': prediction.tolist(),
        'confidence': float(np.max(prediction))
    })

    ch.basic_publish(
        exchange='ml_results',
        routing_key='predictions',
        body=result
    )

    ch.basic_ack(delivery_tag=method.delivery_tag)

channel.queue_declare(queue='ml_requests', durable=True)
channel.basic_consume(queue='ml_requests', on_message_callback=process_prediction)
channel.start_consuming()
```

**Performance**: This architecture achieves:
- 🚀 **4M+ messages/sec** with SQL filters
- ⚡ **Sub-second latency** for model inference
- 📊 **Easy scaling** by adding more workers
- 💾 **Efficient batch processing** for high throughput

</details>

<details>
<summary><b>4. 🔮 OpenAI Integration Pattern</b></summary>

**Use Case**: Queue OpenAI API calls to manage rate limits and costs effectively.

```python
# OpenAI Request Queue Manager
import pika
import openai
import json
import time
from tenacity import retry, wait_exponential, stop_after_attempt

class OpenAIWorker:
    def __init__(self, api_key, rabbitmq_url='amqp://localhost'):
        self.client = openai.OpenAI(api_key=api_key)
        self.connection = pika.BlockingConnection(
            pika.URLParameters(rabbitmq_url)
        )
        self.channel = self.connection.channel()

        # Declare queues with priority
        self.channel.queue_declare(
            queue='openai_requests',
            durable=True,
            arguments={'x-max-priority': 10}
        )

        self.channel.basic_qos(prefetch_count=1)

    @retry(wait=wait_exponential(min=1, max=60), stop=stop_after_attempt(5))
    def process_completion(self, prompt, model='gpt-4', **kwargs):
        """Process OpenAI completion with retry logic"""
        response = self.client.chat.completions.create(
            model=model,
            messages=[{"role": "user", "content": prompt}],
            **kwargs
        )
        return response.choices[0].message.content

    def callback(self, ch, method, properties, body):
        data = json.loads(body)

        try:
            # Process request
            result = self.process_completion(
                prompt=data['prompt'],
                model=data.get('model', 'gpt-4'),
                temperature=data.get('temperature', 0.7),
                max_tokens=data.get('max_tokens', 1000)
            )

            # Publish result
            result_message = json.dumps({
                'request_id': data['request_id'],
                'result': result,
                'model': data.get('model', 'gpt-4'),
                'timestamp': time.time()
            })

            ch.basic_publish(
                exchange='openai_results',
                routing_key=data.get('reply_to', 'default'),
                body=result_message,
                properties=pika.BasicProperties(
                    correlation_id=properties.correlation_id
                )
            )

            ch.basic_ack(delivery_tag=method.delivery_tag)

        except Exception as e:
            # Reject and requeue on failure
            ch.basic_nack(delivery_tag=method.delivery_tag, requeue=True)
            print(f"Error processing request: {e}")

    def start(self):
        self.channel.basic_consume(
            queue='openai_requests',
            on_message_callback=self.callback
        )

        print('🤖 OpenAI Worker started...')
        self.channel.start_consuming()

# Usage
worker = OpenAIWorker(api_key='your-api-key')
worker.start()
```

**Benefits**:
- 💰 **Cost Control**: Rate limiting prevents unexpected API costs
- 🎯 **Priority Queuing**: Process high-priority requests first
- 🔄 **Automatic Retries**: Handle transient API failures gracefully
- 📊 **Request Tracking**: Monitor API usage and costs
- ⚡ **Load Distribution**: Balance requests across multiple API keys

</details>

### 📦 Production-Ready AI/ML Projects

<details>
<summary><b>Click to expand curated AI/ML repositories</b></summary>

#### 🌟 Featured Projects

| Project | Description | Stars | Tech Stack |
|---------|-------------|-------|------------|
| [**celery**](https://github.com/celery/celery) | Distributed task queue for Python | ![Stars](https://img.shields.io/github/stars/celery/celery?style=social) | Python, RabbitMQ, Redis |
| [**dramatiq**](https://github.com/Bogdanp/dramatiq) | Fast and reliable background task processing | ![Stars](https://img.shields.io/github/stars/Bogdanp/dramatiq?style=social) | Python, RabbitMQ |
| [**asynq**](https://github.com/hibiken/asynq) | Simple, reliable task queue in Go | ![Stars](https://img.shields.io/github/stars/hibiken/asynq?style=social) | Go, Redis |
| [**nameko**](https://github.com/nameko/nameko) | Python microservices framework | ![Stars](https://img.shields.io/github/stars/nameko/nameko?style=social) | Python, RabbitMQ |

#### 🎯 ML-Specific Examples

1. **[ml-rabbitmq-pipeline](https://github.com/topics/machine-learning-pipeline)** - Machine Learning pipeline with RabbitMQ
   - Real-time feature engineering
   - Model training orchestration
   - A/B testing infrastructure

2. **[video-analytics-rabbitmq](https://github.com/topics/video-analytics)** - Video analytics with RabbitMQ
   - Frame extraction and queueing
   - Multi-model inference
   - Result aggregation

3. **[nlp-processing-queue](https://github.com/topics/nlp)** - NLP processing with message queues
   - Text preprocessing pipeline
   - Sentiment analysis
   - Named entity recognition

</details>

### 🎓 Best Practices for AI/ML

<details>
<summary><b>Click to expand best practices</b></summary>

#### ✅ Do's

- ✅ **Use priority queues** for different model types (fast vs. slow)
- ✅ **Implement circuit breakers** for model failures
- ✅ **Monitor queue depth** to trigger auto-scaling
- ✅ **Use message TTL** to drop stale predictions
- ✅ **Batch messages** when possible for GPU efficiency
- ✅ **Separate queues** for training vs. inference
- ✅ **Track inference metrics** (latency, throughput, accuracy)
- ✅ **Implement dead letter queues** for failed predictions

#### ❌ Don'ts

- ❌ Don't send large files through messages (use object storage + references)
- ❌ Don't block workers with synchronous preprocessing
- ❌ Don't ignore memory limits on GPU workers
- ❌ Don't use single queue for all model types
- ❌ Don't skip message acknowledgments
- ❌ Don't store model weights in RabbitMQ

#### 📊 Performance Tuning

```python
# Optimized consumer for ML workloads
channel.basic_qos(
    prefetch_count=10,  # Fetch 10 messages at a time
    global_qos=True
)

# Use confirms for critical predictions
channel.confirm_delivery()

# Batch processing
def batch_callback(ch, method, properties, body):
    global batch
    batch.append(json.loads(body))

    if len(batch) >= BATCH_SIZE:
        # Process batch through model
        predictions = model.predict(np.array([msg['features'] for msg in batch]))

        # Publish results
        for msg, pred in zip(batch, predictions):
            publish_result(msg['id'], pred)

        # Acknowledge all messages
        ch.basic_ack(delivery_tag=method.delivery_tag, multiple=True)
        batch = []
```

</details>

---

## 🏗️ Architecture & Design Patterns

<details>
<summary><b>Event-Driven Architecture (EDA)</b></summary>

### Core Patterns

#### 1. 📢 Event Notification
Events notify subscribers when something happens without carrying full state.

```python
# Publisher
channel.exchange_declare(exchange='order_events', exchange_type='topic')

event = {
    'event_type': 'order.created',
    'order_id': '12345',
    'timestamp': time.time()
}

channel.basic_publish(
    exchange='order_events',
    routing_key='order.created',
    body=json.dumps(event)
)
```

#### 2. 📦 Event-Carried State Transfer
Events contain complete state, allowing consumers to maintain local copies.

```python
event = {
    'event_type': 'order.updated',
    'order': {
        'id': '12345',
        'customer_id': 'cust_789',
        'items': [...],
        'total': 99.99,
        'status': 'confirmed'
    },
    'timestamp': time.time()
}
```

#### 3. 📝 Event Sourcing
Store all state changes as sequence of events.

```python
# Event Store Pattern
events = [
    {'type': 'OrderCreated', 'data': {...}, 'sequence': 1},
    {'type': 'ItemAdded', 'data': {...}, 'sequence': 2},
    {'type': 'OrderConfirmed', 'data': {...}, 'sequence': 3}
]

# Replay events to rebuild state
def rebuild_order(order_id):
    state = {}
    for event in get_events(order_id):
        state = apply_event(state, event)
    return state
```

#### 4. 🔄 CQRS (Command Query Responsibility Segregation)

Separate read and write models for better scalability.

```python
# Write Model (Commands)
class OrderCommandHandler:
    def create_order(self, command):
        # Validate and create order
        order = Order.create(command)

        # Publish event
        publish_event('order.created', order.to_dict())

        return order.id

# Read Model (Queries) - Updated by events
class OrderQueryHandler:
    def __init__(self):
        self.read_db = connect_read_database()
        subscribe_to_events('order.*', self.update_read_model)

    def update_read_model(self, event):
        if event['type'] == 'order.created':
            self.read_db.insert(event['data'])
        elif event['type'] == 'order.updated':
            self.read_db.update(event['data'])

    def get_order(self, order_id):
        return self.read_db.get(order_id)
```

</details>

<details>
<summary><b>Saga Pattern</b></summary>

### Distributed Transaction Management

#### Choreography-Based Saga

```python
# Order Service
def create_order(order_data):
    order = save_order(order_data)

    publish_event('order.created', {
        'order_id': order.id,
        'customer_id': order.customer_id,
        'amount': order.total
    })

# Payment Service (listens to order.created)
def handle_order_created(event):
    try:
        payment = process_payment(event['amount'])
        publish_event('payment.completed', {
            'order_id': event['order_id'],
            'payment_id': payment.id
        })
    except PaymentFailed:
        publish_event('payment.failed', {
            'order_id': event['order_id'],
            'reason': 'insufficient_funds'
        })

# Order Service (listens to payment.failed)
def handle_payment_failed(event):
    cancel_order(event['order_id'])
    publish_event('order.cancelled', {
        'order_id': event['order_id'],
        'reason': event['reason']
    })
```

#### Orchestration-Based Saga

```python
# Saga Orchestrator
class OrderSagaOrchestrator:
    def execute(self, order_data):
        saga_id = generate_saga_id()

        try:
            # Step 1: Reserve inventory
            inventory_result = self.call_service(
                'inventory.reserve',
                {'items': order_data['items']},
                timeout=5
            )

            # Step 2: Process payment
            payment_result = self.call_service(
                'payment.process',
                {'amount': order_data['total']},
                timeout=10
            )

            # Step 3: Create order
            order_result = self.call_service(
                'order.create',
                order_data,
                timeout=5
            )

            return {'status': 'completed', 'order_id': order_result['id']}

        except ServiceCallFailed as e:
            # Compensating transactions
            self.rollback(saga_id, e.failed_step)
            return {'status': 'failed', 'reason': str(e)}

    def rollback(self, saga_id, failed_step):
        if failed_step >= 2:
            self.call_service('payment.refund', {...})
        if failed_step >= 1:
            self.call_service('inventory.release', {...})
```

</details>

<details>
<summary><b>Microservices Patterns</b></summary>

### Common Microservices Patterns with RabbitMQ

#### 1. 🔄 Competing Consumers

Multiple workers process messages from same queue.

```python
# Worker 1, 2, 3... all consume from same queue
channel.queue_declare(queue='tasks', durable=True)
channel.basic_qos(prefetch_count=1)

def callback(ch, method, properties, body):
    print(f"Worker {worker_id} processing: {body}")
    time.sleep(body.count(b'.'))  # Simulate work
    ch.basic_ack(delivery_tag=method.delivery_tag)

channel.basic_consume(queue='tasks', on_message_callback=callback)
channel.start_consuming()
```

#### 2. 📮 Request-Reply (RPC)

Synchronous-style communication over async messaging.

```python
# RPC Server
def fib(n):
    return n if n < 2 else fib(n-1) + fib(n-2)

def on_request(ch, method, props, body):
    n = int(body)
    response = fib(n)

    ch.basic_publish(
        exchange='',
        routing_key=props.reply_to,
        properties=pika.BasicProperties(
            correlation_id=props.correlation_id
        ),
        body=str(response)
    )
    ch.basic_ack(delivery_tag=method.delivery_tag)

channel.basic_consume(queue='rpc_queue', on_message_callback=on_request)

# RPC Client
class RpcClient:
    def __init__(self):
        self.connection = pika.BlockingConnection(pika.ConnectionParameters('localhost'))
        self.channel = self.connection.channel()

        result = self.channel.queue_declare(queue='', exclusive=True)
        self.callback_queue = result.method.queue
        self.channel.basic_consume(
            queue=self.callback_queue,
            on_message_callback=self.on_response,
            auto_ack=True
        )

        self.response = None
        self.corr_id = None

    def on_response(self, ch, method, props, body):
        if self.corr_id == props.correlation_id:
            self.response = body

    def call(self, n):
        self.response = None
        self.corr_id = str(uuid.uuid4())

        self.channel.basic_publish(
            exchange='',
            routing_key='rpc_queue',
            properties=pika.BasicProperties(
                reply_to=self.callback_queue,
                correlation_id=self.corr_id
            ),
            body=str(n)
        )

        while self.response is None:
            self.connection.process_data_events()

        return int(self.response)
```

#### 3. ☠️ Dead Letter Exchange (DLQ)

Handle failed messages gracefully.

```python
# Declare queue with DLX
channel.queue_declare(
    queue='main_queue',
    arguments={
        'x-dead-letter-exchange': 'dlx',
        'x-dead-letter-routing-key': 'failed',
        'x-message-ttl': 60000  # 60 seconds
    }
)

# Declare DLX and DLQ
channel.exchange_declare(exchange='dlx', exchange_type='direct')
channel.queue_declare(queue='dead_letter_queue')
channel.queue_bind(exchange='dlx', queue='dead_letter_queue', routing_key='failed')

# Process with rejection to DLQ
def callback(ch, method, properties, body):
    try:
        process_message(body)
        ch.basic_ack(delivery_tag=method.delivery_tag)
    except ProcessingError:
        # Reject - goes to DLQ
        ch.basic_reject(delivery_tag=method.delivery_tag, requeue=False)
```

#### 4. 🎯 Priority Queue

Process high-priority messages first.

```python
# Declare priority queue
channel.queue_declare(
    queue='priority_tasks',
    arguments={'x-max-priority': 10}
)

# Publish with priority
channel.basic_publish(
    exchange='',
    routing_key='priority_tasks',
    body='High priority task',
    properties=pika.BasicProperties(priority=9)
)

channel.basic_publish(
    exchange='',
    routing_key='priority_tasks',
    body='Low priority task',
    properties=pika.BasicProperties(priority=1)
)
```

</details>

---

## 📚 Client Libraries & SDKs

<details open>
<summary><b>Official & Community Libraries</b></summary>

### 🐍 Python

| Library | Protocol | Features | Stars |
|---------|----------|----------|-------|
| [**pika**](https://github.com/pika/pika) | AMQP 0.9.1 | Pure Python, blocking & async | ![Stars](https://img.shields.io/github/stars/pika/pika?style=social) |
| [**aio-pika**](https://github.com/mosquito/aio-pika) | AMQP 0.9.1 | Asyncio-based, high performance | ![Stars](https://img.shields.io/github/stars/mosquito/aio-pika?style=social) |
| [**kombu**](https://github.com/celery/kombu) | AMQP | Messaging library for Python | ![Stars](https://img.shields.io/github/stars/celery/kombu?style=social) |
| [**rabbitmq-amqp-python-client**](https://github.com/rabbitmq/rabbitmq-amqp-python-client) | AMQP 1.0 | Official AMQP 1.0 client | Official |

```bash
pip install pika
pip install aio-pika
```

### 📗 Node.js / TypeScript

| Library | Protocol | Features | Stars |
|---------|----------|----------|-------|
| [**amqplib**](https://github.com/amqp-node/amqplib) | AMQP 0.9.1 | Most popular Node.js client | ![Stars](https://img.shields.io/github/stars/amqp-node/amqplib?style=social) |
| [**rabbitmq-client**](https://www.npmjs.com/package/rabbitmq-client) | AMQP 0.9.1 | Auto-reconnect, TypeScript, zero deps | Popular |
| [**rhea**](https://github.com/amqp/rhea) | AMQP 1.0 | Full AMQP 1.0 implementation | ![Stars](https://img.shields.io/github/stars/amqp/rhea?style=social) |

```bash
npm install amqplib
npm install rabbitmq-client
```

### ☕ Java

| Library | Protocol | Features | Documentation |
|---------|----------|----------|---------------|
| [**rabbitmq-java-client**](https://github.com/rabbitmq/rabbitmq-java-client) | AMQP 0.9.1 | Official Java client, JDK 8+ | [Docs](https://www.rabbitmq.com/client-libraries/java-client) |
| [**Spring AMQP**](https://spring.io/projects/spring-amqp) | AMQP 0.9.1 | Spring Framework integration | [Docs](https://docs.spring.io/spring-amqp/reference/) |
| [**rabbitmq-stream-java-client**](https://github.com/rabbitmq/rabbitmq-stream-java-client) | Streams | RabbitMQ Streams support | Official |

```xml
<dependency>
    <groupId>com.rabbitmq</groupId>
    <artifactId>amqp-client</artifactId>
    <version>5.20.0</version>
</dependency>
```

### 🔷 Go

| Library | Protocol | Features | Stars |
|---------|----------|----------|-------|
| [**amqp091-go**](https://github.com/rabbitmq/amqp091-go) | AMQP 0.9.1 | Official Go client | ![Stars](https://img.shields.io/github/stars/rabbitmq/amqp091-go?style=social) |
| [**rabbitmq-stream-go-client**](https://github.com/rabbitmq/rabbitmq-stream-go-client) | Streams | Stream protocol support | Official |

```bash
go get github.com/rabbitmq/amqp091-go
```

### 💎 Ruby

```bash
gem install bunny  # Most popular
gem install march_hare  # JRuby
```

### 🔵 C# / .NET

```bash
dotnet add package RabbitMQ.Client
dotnet add package RabbitMQ.Stream.Client
```

### 🦀 Rust

```bash
cargo add lapin  # async AMQP client
```

### ⚡ PHP

```bash
composer require php-amqplib/php-amqplib
```

### 🔶 Erlang/Elixir

Built-in support (RabbitMQ is written in Erlang!)

```elixir
{:amqp, "~> 3.3"}  # Elixir
```

</details>

---

## 🔧 Tools & Plugins

<details>
<summary><b>Essential Plugins</b></summary>

### 🔌 Core Plugins

```bash
# Management & Monitoring
rabbitmq-plugins enable rabbitmq_management
rabbitmq-plugins enable rabbitmq_management_agent
rabbitmq-plugins enable rabbitmq_prometheus

# Protocols
rabbitmq-plugins enable rabbitmq_mqtt
rabbitmq-plugins enable rabbitmq_stomp
rabbitmq-plugins enable rabbitmq_web_mqtt
rabbitmq-plugins enable rabbitmq_web_stomp

# Federation & Shovel
rabbitmq-plugins enable rabbitmq_federation
rabbitmq-plugins enable rabbitmq_federation_management
rabbitmq-plugins enable rabbitmq_shovel
rabbitmq-plugins enable rabbitmq_shovel_management

# Streams
rabbitmq-plugins enable rabbitmq_stream
rabbitmq-plugins enable rabbitmq_stream_management

# Additional
rabbitmq-plugins enable rabbitmq_top  # Monitor processes
rabbitmq-plugins enable rabbitmq_tracing  # Debug messages
rabbitmq-plugins enable rabbitmq_consistent_hash_exchange  # Consistent hashing
```

</details>

<details>
<summary><b>Management & Admin Tools</b></summary>

### 🖥️ Web-Based Tools

| Tool | Description | URL |
|------|-------------|-----|
| **RabbitMQ Management** | Built-in web UI | `http://localhost:15672` |
| **RabbitMQ Admin** | CLI-based management | Included with server |
| **RabbitMQ Top** | Real-time process monitor | Plugin-based |

### 📊 CLI Tools

```bash
# rabbitmqctl - Primary management tool
rabbitmqctl status
rabbitmqctl list_queues name messages consumers
rabbitmqctl list_exchanges
rabbitmqctl list_bindings
rabbitmqctl cluster_status
rabbitmqctl node_health_check

# rabbitmqadmin - HTTP API based tool
rabbitmqadmin list queues
rabbitmqadmin declare queue name=my_queue durable=true
rabbitmqadmin publish routing_key=my_queue payload="hello"
rabbitmqadmin get queue=my_queue

# rabbitmq-diagnostics
rabbitmq-diagnostics ping
rabbitmq-diagnostics memory_breakdown
rabbitmq-diagnostics check_alarms
rabbitmq-diagnostics erlang_version
```

### 🐳 Third-Party Tools

| Tool | Description | Link |
|------|-------------|------|
| [**RabbitMQ Perf Test**](https://github.com/rabbitmq/rabbitmq-perf-test) | Load testing tool | Official |
| [**RabbitMQ HTTP API**](https://github.com/rabbitmq/rabbitmq-management) | REST API client | Official |
| [**Bunny Burrow**](https://github.com/bytemunch/bunny-burrow) | Modern GUI for RabbitMQ | Community |

</details>

---

## 📊 Monitoring & Observability

<details open>
<summary><b>Prometheus & Grafana Setup</b></summary>

### 🎯 Quick Setup

```bash
# Enable Prometheus plugin
rabbitmq-plugins enable rabbitmq_prometheus

# Verify metrics endpoint
curl http://localhost:15692/metrics
```

### 📝 Prometheus Configuration

```yaml
# prometheus.yml
global:
  scrape_interval: 30s
  evaluation_interval: 30s

scrape_configs:
  - job_name: 'rabbitmq'
    static_configs:
      - targets: ['rabbitmq:15692']
    relabel_configs:
      - source_labels: [__address__]
        target_label: instance
        regex: '([^:]+):.*'
        replacement: '${1}'
```

### 📈 Grafana Dashboards

**Pre-built Dashboards**:
- [RabbitMQ Overview](https://grafana.com/grafana/dashboards/4279) - Comprehensive overview
- [RabbitMQ Cluster](https://grafana.com/grafana/dashboards/2121) - Cluster monitoring
- [RabbitMQ Streams](https://grafana.com/grafana/dashboards/15691) - Stream metrics

**Key Metrics to Monitor**:

| Metric | Description | Alert Threshold |
|--------|-------------|-----------------|
| `rabbitmq_queue_messages` | Messages in queue | > 10,000 |
| `rabbitmq_connections` | Active connections | > 1,000 |
| `rabbitmq_consumers` | Active consumers | < expected |
| `rabbitmq_global_messages_unacknowledged_total` | Unacked messages | > 5,000 |
| `rabbitmq_process_resident_memory_bytes` | Memory usage | > 80% of limit |
| `rabbitmq_disk_space_available_bytes` | Free disk space | < 2GB |
| `rabbitmq_queue_consumer_utilisation` | Consumer utilization | < 0.8 |

</details>

<details>
<summary><b>Recommended Alerts</b></summary>

```yaml
# prometheus-alerts.yml
groups:
  - name: rabbitmq
    interval: 30s
    rules:
      - alert: RabbitMQHighQueueSize
        expr: rabbitmq_queue_messages > 10000
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "High queue size on {{ $labels.queue }}"
          description: "Queue {{ $labels.queue }} has {{ $value }} messages"

      - alert: RabbitMQNoConsumers
        expr: rabbitmq_queue_consumers == 0 and rabbitmq_queue_messages > 0
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "No consumers on queue {{ $labels.queue }}"

      - alert: RabbitMQHighMemoryUsage
        expr: rabbitmq_process_resident_memory_bytes / rabbitmq_resident_memory_limit_bytes > 0.9
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "High memory usage on {{ $labels.instance }}"

      - alert: RabbitMQNodeDown
        expr: up{job="rabbitmq"} == 0
        for: 1m
        labels:
          severity: critical
        annotations:
          summary: "RabbitMQ node {{ $labels.instance }} is down"
```

</details>

---

## 📖 Learning Resources

<details>
<summary><b>Official Documentation</b></summary>

### 📚 Core Documentation

- [**Official Documentation**](https://www.rabbitmq.com/docs) - Comprehensive guides and references
- [**AMQP 0.9.1 Reference**](https://www.rabbitmq.com/amqp-0-9-1-reference.html) - Protocol specification
- [**Best Practices**](https://www.rabbitmq.com/best-practices) - Production guidelines
- [**Release Information**](https://www.rabbitmq.com/release-information) - Version history and upgrades

### 🎓 Getting Started

- [**RabbitMQ for Beginners**](https://www.cloudamqp.com/blog/part1-rabbitmq-for-beginners-what-is-rabbitmq.html) - CloudAMQP series
- [**Free Online Training**](https://training.cloudamqp.com/) - Interactive step-by-step guide
- [**Getting Started eBook**](https://www.cloudamqp.com/rabbitmq_ebook.html) - Free downloadable guide

</details>

<details>
<summary><b>Books & eBooks</b></summary>

### 📕 Recommended Books

1. **RabbitMQ in Depth** by Gavin M. Roy
   - Comprehensive guide to RabbitMQ
   - Advanced patterns and best practices
   - Production deployment strategies

2. **RabbitMQ Essentials** by Lovisa Johansson & David Dossot
   - Quick start guide
   - Practical examples
   - Real-world use cases

3. **Microservices Patterns** by Chris Richardson
   - Saga pattern implementation
   - Event-driven architectures
   - RabbitMQ integration patterns

4. **Enterprise Integration Patterns** by Gregor Hohpe
   - Foundational messaging patterns
   - Architecture design principles
   - Still relevant after 20 years

</details>

<details>
<summary><b>Blogs & Articles</b></summary>

### ✍️ Technical Blogs

- [**RabbitMQ Official Blog**](https://www.rabbitmq.com/blog) - Latest updates and announcements
- [**CloudAMQP Blog**](https://www.cloudamqp.com/blog) - Tutorials and best practices
- [**Theodo Blog - Event-Driven Architectures**](https://blog.theodo.com/2019/08/event-driven-architectures-rabbitmq/)
- [**Medium - RabbitMQ Tag**](https://medium.com/tag/rabbitmq) - Community articles

### 📰 Must-Read Articles

1. [**Deploying RabbitMQ to Kubernetes**](https://www.rabbitmq.com/blog/2020/08/10/deploying-rabbitmq-to-kubernetes-whats-involved)
2. [**Event-Driven Microservices**](https://medium.com/aspnetrun/microservices-event-driven-architecture-with-rabbitmq-and-docker-container-on-net-968d73052cbb)
3. [**CQRS and Saga Patterns**](https://medium.com/@ingila185/cqrs-and-saga-the-essential-patterns-for-high-performance-microservice-4f23a09889b4)

</details>

---

## 🎓 Tutorials & Courses

<details open>
<summary><b>Official Tutorials</b></summary>

### 🐰 RabbitMQ Official Tutorials

[**Official Tutorial Series**](https://www.rabbitmq.com/tutorials) - Available in multiple languages:

1. **Hello World** - Basic producer and consumer
2. **Work Queues** - Distributing tasks among workers
3. **Publish/Subscribe** - Sending messages to many consumers
4. **Routing** - Receiving messages selectively
5. **Topics** - Pattern-based message routing
6. **RPC** - Request/reply pattern
7. **Publisher Confirms** - Reliable publishing

**Languages**: Java, Python, Go, Ruby, JavaScript, C#, PHP, Elixir

</details>

<details>
<summary><b>Online Courses</b></summary>

### 🎥 Video Courses

#### Pluralsight

- [**RabbitMQ by Example**](https://www.pluralsight.com/courses/rabbitmq-by-example)
  - Practical examples with real scenarios
  - Card payments and purchase orders
  - Intermediate level

- **Working with RabbitMQ**
  - Task queue fundamentals
  - Asynchronous processing
  - File transcoding examples

#### Udemy

- [**Learn RabbitMQ: In-Depth Concepts from Scratch**](https://www.udemy.com/course/rabbitmq-message-broker-learn-in-depth-concepts-in-rabbitmq/)
  - ⭐ 4.0/5 rating (1,757 reviews)
  - 50% theory, 50% demos
  - Animated presentations

- **RabbitMQ and Messaging Concepts**
  - 4 hours of content
  - Beginner to advanced
  - Hands-on projects

- [**Event-Driven Microservices, CQRS, SAGA, Axon, Spring Boot**](https://www.udemy.com/course/spring-boot-microservices-cqrs-saga-axon-framework/)
  - Advanced patterns
  - Spring Boot integration
  - Production-ready examples

#### Class Central

[**100+ RabbitMQ Courses**](https://www.classcentral.com/subject/rabbitmq)
- Java & Spring Boot integration
- Python implementations
- Node.js examples
- Performance optimization

</details>

<details>
<summary><b>Interactive Learning</b></summary>

### 💻 Hands-On Practice

- [**CloudAMQP Online Training**](https://training.cloudamqp.com/)
  - Step-by-step interactive tutorials
  - Set up connections
  - Publish and subscribe to messages
  - Free to use

- [**Katacoda Scenarios**](https://katacoda.com/)
  - Browser-based learning environment
  - Pre-configured RabbitMQ instances
  - Practical exercises

</details>

---

## ⚡ Performance & Optimization

<details>
<summary><b>Performance Tuning</b></summary>

### 🚀 Configuration Optimization

```ini
# rabbitmq.conf - Production Optimizations

# Network & Connections
channel_max = 2048
heartbeat = 60
frame_max = 131072

# Memory Management
vm_memory_high_watermark.relative = 0.6
vm_memory_high_watermark_paging_ratio = 0.75
total_memory_available_override_value = 4GB

# Disk Management
disk_free_limit.absolute = 2GB
disk_free_limit.relative = 1.0

# Queue Performance
queue_index_embed_msgs_below = 4096
queue_master_locator = min-masters

# Message Store
msg_store_file_size_limit = 16777216

# Clustering
cluster_partition_handling = autoheal
cluster_keepalive_interval = 10000

# Logging (reduce for production)
log.console.level = warning
```

### 📊 Performance Benchmarks

**RabbitMQ 4.2 Performance** (default configuration):
- **Message Throughput**: ~50,000 messages/second
- **With SQL Filters**: 4,000,000+ messages/second
- **Latency**: ~1-5ms (p50), ~10-20ms (p99)
- **Connections**: Support for 10,000+ concurrent connections

**Optimization Tips**:

```python
# 1. Use prefetch for consumers
channel.basic_qos(prefetch_count=10)

# 2. Publisher confirms for reliability
channel.confirm_delivery()

# 3. Batch publishing
properties = pika.BasicProperties(delivery_mode=2)
for msg in messages:
    channel.basic_publish(
        exchange='',
        routing_key='queue',
        body=msg,
        properties=properties
    )

# 4. Use lazy queues for large queues
channel.queue_declare(
    queue='large_queue',
    arguments={'x-queue-mode': 'lazy'}
)

# 5. Connection pooling
from pika.pool import QueuedPool
pool = QueuedPool(
    create=lambda: pika.BlockingConnection(parameters),
    max_size=10,
    max_overflow=10,
    timeout=10,
    recycle=3600
)
```

</details>

<details>
<summary><b>Scalability Patterns</b></summary>

### 📈 Horizontal Scaling

```bash
# Add nodes to cluster
rabbitmqctl stop_app
rabbitmqctl join_cluster rabbit@node1
rabbitmqctl start_app

# Check cluster status
rabbitmqctl cluster_status

# Enable HA queues
rabbitmqctl set_policy ha-all ".*" '{"ha-mode":"all"}'
```

### 🔄 Load Balancing

```nginx
# nginx.conf - Load balance AMQP connections
stream {
    upstream rabbitmq_cluster {
        server rabbitmq1:5672;
        server rabbitmq2:5672;
        server rabbitmq3:5672;
    }

    server {
        listen 5672;
        proxy_pass rabbitmq_cluster;
        proxy_connect_timeout 1s;
    }
}
```

### 📊 Sharding Plugin

```bash
# Enable sharding
rabbitmq-plugins enable rabbitmq_sharding

# Create sharded exchange
rabbitmqadmin declare exchange name=sharded_exchange type=x-modulus-hash \
    arguments='{"shards-per-node": 2}'
```

</details>

---

## 🔒 Security Best Practices

<details>
<summary><b>Authentication & Authorization</b></summary>

### 🔐 User Management

```bash
# Create users with strong passwords
rabbitmqctl add_user app_user $(openssl rand -base64 32)
rabbitmqctl set_user_tags app_user monitoring

# Grant minimal permissions
rabbitmqctl set_permissions -p production app_user "^app\..*" "^app\..*" "^app\..*"

# List users and permissions
rabbitmqctl list_users
rabbitmqctl list_permissions -p production
```

### 🛡️ TLS/SSL Configuration

```ini
# rabbitmq.conf
listeners.ssl.default = 5671

ssl_options.cacertfile = /path/to/ca_certificate.pem
ssl_options.certfile   = /path/to/server_certificate.pem
ssl_options.keyfile    = /path/to/server_key.pem
ssl_options.verify     = verify_peer
ssl_options.fail_if_no_peer_cert = true

ssl_options.versions.1 = tlsv1.3
ssl_options.versions.2 = tlsv1.2
```

### 🔑 Authentication Backends

```bash
# LDAP Authentication
rabbitmq-plugins enable rabbitmq_auth_backend_ldap

# OAuth 2.0
rabbitmq-plugins enable rabbitmq_auth_backend_oauth2

# HTTP Backend
rabbitmq-plugins enable rabbitmq_auth_backend_http
```

</details>

<details>
<summary><b>Network Security</b></summary>

### 🌐 Firewall Rules

```bash
# Allow only necessary ports
ufw allow 5672/tcp   # AMQP
ufw allow 5671/tcp   # AMQP over TLS
ufw allow 15672/tcp  # Management UI (restrict to internal network)
ufw allow 25672/tcp  # Inter-node communication (cluster only)
```

### 🔒 Virtual Host Isolation

```bash
# Create separate vhosts for different environments
rabbitmqctl add_vhost production
rabbitmqctl add_vhost staging
rabbitmqctl add_vhost development

# Isolate user access
rabbitmqctl set_permissions -p production prod_user ".*" ".*" ".*"
rabbitmqctl set_permissions -p staging staging_user ".*" ".*" ".*"
```

</details>

---

## 🆚 Comparisons

<details open>
<summary><b>RabbitMQ vs Kafka vs Redis</b></summary>

### 📊 Feature Comparison

| Feature | RabbitMQ | Apache Kafka | Redis |
|---------|----------|--------------|-------|
| **Throughput** | ~50K msgs/sec | ~1M msgs/sec | ~100K msgs/sec |
| **Latency** | 1-5ms | 5-10ms | <1ms |
| **Message Retention** | Until consumed | Configurable (days/weeks) | None (in-memory) |
| **Persistence** | Optional | Yes (disk-based) | Optional (dump to disk) |
| **Ordering Guarantee** | Per queue | Per partition | Per channel |
| **Message Replay** | Limited | Yes (time-based) | No |
| **Protocol** | AMQP, MQTT, STOMP | Custom binary | Redis protocol |
| **Use Case** | Task queues, RPC | Event streaming, logs | Cache, pub/sub |
| **Clustering** | Native support | Native support | Redis Cluster |
| **Learning Curve** | Medium | Steep | Easy |
| **Delivery Guarantee** | At-most/at-least/exactly-once | At-least-once | At-most-once |

### 🎯 When to Use What

#### Use RabbitMQ When:
- ✅ You need traditional message queue patterns
- ✅ Complex routing requirements (topic exchanges)
- ✅ Priority queues are important
- ✅ You need strong delivery guarantees
- ✅ Request/reply (RPC) patterns
- ✅ You want mature, production-ready solution
- ✅ Multiple protocol support needed

#### Use Kafka When:
- ✅ High-throughput event streaming
- ✅ Need to replay messages
- ✅ Log aggregation and processing
- ✅ Real-time analytics pipeline
- ✅ Long-term message retention
- ✅ Event sourcing architecture
- ✅ Need exactly-once semantics

#### Use Redis When:
- ✅ Ultra-low latency required (<1ms)
- ✅ Simple pub/sub without persistence
- ✅ Message loss is acceptable
- ✅ You also need caching
- ✅ Short-lived messages
- ✅ High-speed, in-memory processing

### 💰 Cost Comparison

| Aspect | RabbitMQ | Kafka | Redis |
|--------|----------|-------|-------|
| **Memory** | Medium | Low | High |
| **Disk** | Medium | High | Low |
| **CPU** | Medium | Medium-High | Low |
| **Operational Complexity** | Medium | High | Low |

</details>

---

## 🌟 Awesome Projects

<details>
<summary><b>Production-Ready Frameworks</b></summary>

### 🐍 Python

| Project | Description | Stars |
|---------|-------------|-------|
| [**Celery**](https://github.com/celery/celery) | Distributed task queue | ![Stars](https://img.shields.io/github/stars/celery/celery?style=social) |
| [**Dramatiq**](https://github.com/Bogdanp/dramatiq) | Fast distributed task processing | ![Stars](https://img.shields.io/github/stars/Bogdanp/dramatiq?style=social) |
| [**Nameko**](https://github.com/nameko/nameko) | Microservices framework | ![Stars](https://img.shields.io/github/stars/nameko/nameko?style=social) |
| [**Kombu**](https://github.com/celery/kombu) | Messaging library | ![Stars](https://img.shields.io/github/stars/celery/kombu?style=social) |

### 📗 Node.js

| Project | Description | Stars |
|---------|-------------|-------|
| [**Bull**](https://github.com/OptimalBits/bull) | Premium queue package (uses Redis) | ![Stars](https://img.shields.io/github/stars/OptimalBits/bull?style=social) |
| [**BullMQ**](https://github.com/taskforcesh/bullmq) | Modern Bull successor | ![Stars](https://img.shields.io/github/stars/taskforcesh/bullmq?style=social) |
| [**jackrabbit**](https://github.com/hunterloftis/jackrabbit) | Easy RabbitMQ for Node.js | ![Stars](https://img.shields.io/github/stars/hunterloftis/jackrabbit?style=social) |

### ☕ Java / Spring

| Project | Description | Link |
|---------|-------------|------|
| **Spring AMQP** | Spring Framework AMQP support | [spring.io](https://spring.io/projects/spring-amqp) |
| **Spring Cloud Stream** | Event-driven microservices | [spring.io](https://spring.io/projects/spring-cloud-stream) |

### 🔷 Go

| Project | Description | Stars |
|---------|-------------|-------|
| [**Asynq**](https://github.com/hibiken/asynq) | Simple, reliable task queue | ![Stars](https://img.shields.io/github/stars/hibiken/asynq?style=social) |
| [**Machinery**](https://github.com/RichardKnop/machinery) | Async task queue/job queue | ![Stars](https://img.shields.io/github/stars/RichardKnop/machinery?style=social) |

</details>

<details>
<summary><b>Curated Lists</b></summary>

- [**awesome-rabbitmq**](https://github.com/niamtokik/awesome-rabbitmq) - Comprehensive RabbitMQ resources
- [**awesome-software-architecture**](https://github.com/mehdihadeli/awesome-software-architecture/blob/main/docs/messaging/rabbitmq.md) - RabbitMQ in software architecture

</details>

<details>
<summary><b>Example Projects</b></summary>

### 🎯 Real-World Examples

1. **E-Commerce Order Processing**
   ```
   Order Service → RabbitMQ → [Payment, Inventory, Shipping] Services
   ```

2. **Video Processing Pipeline**
   ```
   Upload → RabbitMQ → [Transcoding, Thumbnail, AI Analysis] Workers
   ```

3. **Microservices Event Bus**
   ```
   Services ↔ RabbitMQ (Event Exchange) ↔ Services
   ```

4. **IoT Data Collection**
   ```
   IoT Devices → MQTT → RabbitMQ → [Storage, Analytics, Alerts]
   ```

</details>

---

## 🤝 Contributing

We welcome contributions from the community! Here's how you can help:

### 📝 How to Contribute

1. **Fork** this repository
2. **Create** a new branch (`git checkout -b feature/amazing-resource`)
3. **Add** your awesome resource
4. **Commit** your changes (`git commit -m 'Add amazing RabbitMQ resource'`)
5. **Push** to the branch (`git push origin feature/amazing-resource`)
6. **Open** a Pull Request

### ✅ Contribution Guidelines

- Ensure links are valid and resources are high-quality
- Add resources in the appropriate category
- Use consistent formatting
- Include brief descriptions
- For projects, include GitHub stars badge
- Verify content is up-to-date and relevant

### 🎯 What to Contribute

- 📚 Tutorials and learning resources
- 🔧 Tools and plugins
- 💡 Best practices and patterns
- 🐛 Bug fixes in documentation
- 🌟 Awesome projects using RabbitMQ
- 📖 Books and courses
- 🎥 Videos and talks

---

## 📜 License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

To the extent possible under law, the contributors have waived all copyright and related or neighboring rights to this work.

---

<div align="center">

### ⭐ Star this repository if you find it helpful!

**Made with ❤️ by the RabbitMQ community**

[Back to Top ⬆️](#-awesome-rabbitmq-)

---

**Latest Update**: 2025-11-17 | **Contributors**: Growing community

</div>
