# 🤖 Redis for AI Agents - Complete Integration Guide

> **Building Production-Ready AI Agent Systems with Redis**
> Ultra-low latency memory, semantic caching, and vector search for intelligent agents

[![Redis](https://img.shields.io/badge/Redis-8.0-DC382D?style=for-the-badge&logo=redis&logoColor=white)](https://redis.io)
[![AI](https://img.shields.io/badge/AI-Agents-00D9FF?style=for-the-badge&logo=openai&logoColor=white)](https://redis.io/redis-for-ai/)
[![LangChain](https://img.shields.io/badge/LangChain-Integrated-121212?style=for-the-badge&logo=chainlink&logoColor=white)](https://python.langchain.com/)

---

## 📋 Table of Contents

- [Why Redis for AI Agents?](#why-redis-for-ai-agents)
- [Redis AI Agent Architecture](#redis-ai-agent-architecture)
- [LangCache - Semantic Caching](#langcache---semantic-caching)
- [RedisVL - Vector Database](#redisvl---vector-database)
- [Agent Memory Management](#agent-memory-management)
- [LangChain & LangGraph Integration](#langchain--langgraph-integration)
- [AutoGen & CrewAI Integration](#autogen--crewai-integration)
- [Redis Streams for Event-Driven Agents](#redis-streams-for-event-driven-agents)
- [Production Case Studies](#production-case-studies)
- [Best Practices](#best-practices)
- [Example Applications](#example-applications)

---

## 🎯 Why Redis for AI Agents?

Redis has emerged as the **#1 choice** for AI agent infrastructure in 2025, with **43% of developers** using Redis for agent memory and data storage (Stack Overflow Survey 2025).

### Key Advantages

```
┌─────────────────────────────────────────────┐
│      REDIS FOR AI AGENTS - KEY BENEFITS     │
├─────────────────────────────────────────────┤
│ ⚡ Ultra-Low Latency     │ <1ms responses   │
│ 🧠 Multi-Type Memory     │ Short + Long     │
│ 💰 Cost Reduction        │ 70-90% savings   │
│ 🔍 Vector Search         │ Semantic recall  │
│ 🎯 Semantic Caching      │ LangCache        │
│ 🔄 Event Streaming       │ Redis Streams    │
│ 🌐 Production Scale      │ 1M+ ops/sec      │
│ 🔌 Framework Support     │ All major ones   │
└─────────────────────────────────────────────┘
```

### Redis vs Other Solutions

| Feature | Redis | Traditional DB | Vector-Only DB |
|---------|-------|----------------|----------------|
| **Latency** | **<1ms** | ~50-100ms | ~10-20ms |
| **Memory Types** | **All 3 types** | Limited | Long-term only |
| **Caching** | **Native (LangCache)** | Manual | None |
| **Pub/Sub** | **Built-in** | Limited | None |
| **Streams** | **Yes** | Limited | No |
| **Vector Search** | **Yes (RedisVL)** | No | Yes |
| **Framework Integration** | **Extensive** | Limited | Growing |
| **Developer Adoption** | **43%** | Various | 10-15% |

### Three Types of Agent Memory

```
┌────────────────────────────────────────────────────┐
│              AGENT MEMORY HIERARCHY                │
└────────────────────────────────────────────────────┘

1️⃣ SHORT-TERM MEMORY (Working Context)
   ┌──────────────────────────────────┐
   │ • Current conversation           │
   │ • Active task context            │
   │ • Session-specific data          │
   │ Storage: Redis Strings/Hashes    │
   │ TTL: Minutes to hours            │
   └──────────────────────────────────┘

2️⃣ LONG-TERM MEMORY (Semantic Recall)
   ┌──────────────────────────────────┐
   │ • Historical conversations       │
   │ • Learned user preferences       │
   │ • Domain knowledge               │
   │ Storage: RedisVL (Vectors)       │
   │ TTL: Days to permanent           │
   └──────────────────────────────────┘

3️⃣ STRUCTURED MEMORY (Facts & State)
   ┌──────────────────────────────────┐
   │ • User profiles                  │
   │ • Configuration                  │
   │ • Agent state                    │
   │ Storage: Redis Hashes/JSON       │
   │ TTL: Persistent                  │
   └──────────────────────────────────┘
```

---

## 🏗️ Redis AI Agent Architecture

### Single Agent with Redis Memory

```
┌─────────────────────────────────────────────────────┐
│                    USER REQUEST                     │
└────────────────┬────────────────────────────────────┘
                 │
                 ▼
┌────────────────────────────────────────────────────┐
│              AI AGENT (LLM)                        │
│  ┌──────────────────────────────────────────┐     │
│  │  1. Retrieve context from memory         │     │
│  │  2. Check semantic cache                 │     │
│  │  3. Process with LLM (if cache miss)     │     │
│  │  4. Update memory                        │     │
│  └──────────────────────────────────────────┘     │
└────────────────┬───────────────────────────────────┘
                 │
                 ▼
┌────────────────────────────────────────────────────┐
│                  REDIS MEMORY LAYER                │
│  ┌─────────────┐  ┌─────────────┐  ┌───────────┐ │
│  │ LangCache   │  │  RedisVL    │  │  Hashes   │ │
│  │ (Semantic)  │  │ (Vectors)   │  │  (State)  │ │
│  │             │  │             │  │           │ │
│  │ 90% cache   │  │ Similarity  │  │ User      │ │
│  │ hit rate    │  │ search      │  │ profiles  │ │
│  └─────────────┘  └─────────────┘  └───────────┘ │
└────────────────────────────────────────────────────┘
                 │
                 ▼
        ┌────────────────┐
        │  RESPONSE      │
        │  (Fast + Smart)│
        └────────────────┘
```

### Multi-Agent System with Redis Coordination

```
┌────────────────────────────────────────────────────┐
│              ORCHESTRATOR AGENT                    │
│         (Task Decomposition & Routing)             │
└──────┬─────────────┬─────────────┬─────────────────┘
       │             │             │
   ┌───▼───┐    ┌───▼───┐    ┌───▼────┐
   │Agent 1│    │Agent 2│    │Agent 3 │
   │(Search)│   │(Analyze)│  │(Write) │
   └───┬───┘    └───┬───┘    └───┬────┘
       │             │             │
       └─────────────┴─────────────┘
                     │
                     ▼
    ┌────────────────────────────────────┐
    │       REDIS - SHARED MEMORY        │
    │                                    │
    │  • Agent-to-agent communication    │
    │  • Shared context & state          │
    │  • Event streams (coordination)    │
    │  • Vector memory (knowledge base)  │
    └────────────────────────────────────┘
```

### Real-Time RAG with Redis

```
┌──────────────────────────────────────────────────┐
│           USER QUERY                             │
│  "What are Redis 8 new features?"                │
└────────────┬─────────────────────────────────────┘
             │
             ▼
┌────────────────────────────────────────────────┐
│  1. SEMANTIC CACHE CHECK (LangCache)           │
│     Similar question cached? → Return instantly│
└────────────┬───────────────────────────────────┘
             │ Cache Miss
             ▼
┌────────────────────────────────────────────────┐
│  2. VECTOR SEARCH (RedisVL)                    │
│     Find relevant docs via embedding similarity│
│     Cosine distance < 0.1                      │
└────────────┬───────────────────────────────────┘
             │
             ▼
┌────────────────────────────────────────────────┐
│  3. LLM GENERATION                             │
│     Combine retrieved context + query          │
│     Generate answer with GPT-4                 │
└────────────┬───────────────────────────────────┘
             │
             ▼
┌────────────────────────────────────────────────┐
│  4. CACHE RESPONSE (LangCache)                 │
│     Store for future similar queries          │
│     TTL: 24 hours                              │
└────────────┬───────────────────────────────────┘
             │
             ▼
┌────────────────────────────────────────────────┐
│         RESPONSE TO USER                       │
│  Latency: <100ms (vs 2-5s without cache)      │
│  Cost: $0 (vs $0.05 per LLM call)             │
└────────────────────────────────────────────────┘
```

---

## 💰 LangCache - Semantic Caching

**LangCache** is Redis's fully-managed semantic caching service that reduces LLM costs by **70-90%** and improves response times by **100-1000x**.

### How LangCache Works

Instead of exact string matching, LangCache uses **semantic similarity** to identify similar questions:

```python
from langchain_redis import LangCache
from openai import OpenAI
import os

# Initialize LangCache
cache = LangCache(
    redis_url=os.getenv("REDIS_URL", "redis://localhost:6379"),
    ttl=3600,  # Cache for 1 hour
    distance_threshold=0.1,  # Similarity threshold (lower = more strict)
    embeddings_provider="openai",  # or "cohere", "huggingface"
    embeddings_model="text-embedding-ada-002"
)

client = OpenAI()

def ask_with_cache(question: str) -> str:
    """Ask LLM with semantic caching"""

    # Check cache first
    cached_response = cache.get(question)
    if cached_response:
        print("✅ Cache HIT! Returning cached response")
        return cached_response

    print("❌ Cache MISS. Calling LLM...")

    # Call LLM (expensive)
    response = client.chat.completions.create(
        model="gpt-4",
        messages=[{
            "role": "user",
            "content": question
        }]
    )

    answer = response.choices[0].message.content

    # Store in cache
    cache.set(question, answer)

    return answer

# Example usage
# First call - cache miss
q1 = "What is machine learning?"
answer1 = ask_with_cache(q1)
# ❌ Cache MISS. Calling LLM...
# Latency: 2.5s, Cost: $0.05

# Similar question - cache hit!
q2 = "Explain ML to me"  # Semantically similar
answer2 = ask_with_cache(q2)
# ✅ Cache HIT! Returning cached response
# Latency: 5ms, Cost: $0.00
# 🎉 500x faster, 100% cost savings!

# Very similar question - still hits cache
q3 = "Can you tell me about machine learning?"
answer3 = ask_with_cache(q3)
# ✅ Cache HIT!
```

### Cost Savings Calculator

```python
def calculate_langcache_savings(
    monthly_requests: int,
    cache_hit_rate: float,  # 0.0 to 1.0
    cost_per_output_token: float = 0.00006,  # GPT-4
    avg_output_tokens: int = 500
):
    """Calculate monthly savings with LangCache"""

    # Without cache
    total_llm_calls = monthly_requests
    monthly_cost_without_cache = (
        total_llm_calls * avg_output_tokens * cost_per_output_token
    )

    # With cache
    cache_hits = monthly_requests * cache_hit_rate
    cache_misses = monthly_requests * (1 - cache_hit_rate)
    monthly_cost_with_cache = (
        cache_misses * avg_output_tokens * cost_per_output_token
    )

    # Savings
    monthly_savings = monthly_cost_without_cache - monthly_cost_with_cache
    savings_percentage = (monthly_savings / monthly_cost_without_cache) * 100

    print(f"📊 LangCache Savings Analysis")
    print(f"━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━")
    print(f"Monthly Requests:     {monthly_requests:,}")
    print(f"Cache Hit Rate:       {cache_hit_rate*100:.1f}%")
    print(f"")
    print(f"WITHOUT Cache:")
    print(f"  Total LLM Calls:    {total_llm_calls:,}")
    print(f"  Monthly Cost:       ${monthly_cost_without_cache:,.2f}")
    print(f"")
    print(f"WITH LangCache:")
    print(f"  Cache Hits:         {cache_hits:,.0f}")
    print(f"  LLM Calls:          {cache_misses:,.0f}")
    print(f"  Monthly Cost:       ${monthly_cost_with_cache:,.2f}")
    print(f"")
    print(f"💰 SAVINGS:")
    print(f"  Monthly:            ${monthly_savings:,.2f}")
    print(f"  Annual:             ${monthly_savings*12:,.2f}")
    print(f"  Percentage:         {savings_percentage:.1f}%")

# Example: 1M requests/month with 80% cache hit rate
calculate_langcache_savings(
    monthly_requests=1_000_000,
    cache_hit_rate=0.80
)

# Output:
# 📊 LangCache Savings Analysis
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# Monthly Requests:     1,000,000
# Cache Hit Rate:       80.0%
#
# WITHOUT Cache:
#   Total LLM Calls:    1,000,000
#   Monthly Cost:       $30,000.00
#
# WITH LangCache:
#   Cache Hits:         800,000
#   LLM Calls:          200,000
#   Monthly Cost:       $6,000.00
#
# 💰 SAVINGS:
#   Monthly:            $24,000.00
#   Annual:             $288,000.00
#   Percentage:         80.0%
```

### Production LangCache Deployment

```python
from langchain_redis import LangCache
from langchain_openai import ChatOpenAI, OpenAIEmbeddings
from langchain.schema import HumanMessage
import logging

# Configure logging
logging.basicConfig(level=logging.INFO)
logger = logging.getLogger(__name__)

class ProductionAgent:
    def __init__(
        self,
        redis_url: str,
        cache_ttl: int = 3600,
        distance_threshold: float = 0.1
    ):
        # Initialize LangCache
        self.cache = LangCache(
            redis_url=redis_url,
            ttl=cache_ttl,
            distance_threshold=distance_threshold,
            embeddings=OpenAIEmbeddings(model="text-embedding-ada-002")
        )

        # Initialize LLM
        self.llm = ChatOpenAI(
            model="gpt-4",
            temperature=0.7,
            max_tokens=500
        )

        # Metrics
        self.cache_hits = 0
        self.cache_misses = 0

    def query(self, user_input: str) -> dict:
        """Process user query with semantic caching"""

        # Check cache
        cached = self.cache.get(user_input)

        if cached:
            self.cache_hits += 1
            logger.info(f"✅ Cache HIT (hit rate: {self.hit_rate():.1%})")
            return {
                "response": cached,
                "cached": True,
                "latency_ms": 5,  # Approximate
                "cost": 0.0
            }

        # Cache miss - call LLM
        self.cache_misses += 1
        logger.info(f"❌ Cache MISS (hit rate: {self.hit_rate():.1%})")

        import time
        start = time.time()

        response = self.llm.invoke([HumanMessage(content=user_input)])
        answer = response.content

        latency = (time.time() - start) * 1000

        # Store in cache
        self.cache.set(user_input, answer)

        return {
            "response": answer,
            "cached": False,
            "latency_ms": latency,
            "cost": 0.05  # Approximate for GPT-4
        }

    def hit_rate(self) -> float:
        """Calculate cache hit rate"""
        total = self.cache_hits + self.cache_misses
        return self.cache_hits / total if total > 0 else 0.0

    def stats(self) -> dict:
        """Get cache statistics"""
        return {
            "cache_hits": self.cache_hits,
            "cache_misses": self.cache_misses,
            "hit_rate": self.hit_rate(),
            "total_queries": self.cache_hits + self.cache_misses
        }

# Usage
agent = ProductionAgent(redis_url="redis://localhost:6379")

# Simulate user queries
questions = [
    "What is Redis?",
    "Explain Redis to me",  # Similar to first
    "How does Redis work?",
    "Tell me about Redis",  # Similar to first/second
    "What are Redis use cases?",
]

for q in questions:
    result = agent.query(q)
    print(f"Q: {q}")
    print(f"Cached: {result['cached']}, Latency: {result['latency_ms']:.0f}ms")
    print()

# Print stats
stats = agent.stats()
print(f"📊 Cache Statistics:")
print(f"  Total Queries: {stats['total_queries']}")
print(f"  Cache Hits:    {stats['cache_hits']}")
print(f"  Cache Misses:  {stats['cache_misses']}")
print(f"  Hit Rate:      {stats['hit_rate']:.1%}")
```

---

## 🔍 RedisVL - Vector Database

**RedisVL** (Redis Vector Library) is a dedicated Python client for building production-ready vector search applications.

### Installation & Setup

```bash
pip install redisvl openai
```

### Basic Vector Search

```python
from redisvl.index import SearchIndex
from redisvl.query import VectorQuery
from openai import OpenAI
import numpy as np

# Initialize OpenAI client
client = OpenAI()

def get_embedding(text: str) -> list:
    """Generate embedding for text"""
    response = client.embeddings.create(
        model="text-embedding-ada-002",
        input=text
    )
    return response.data[0].embedding

# Define index schema
schema = {
    "index": {
        "name": "docs_index",
        "prefix": "doc",
        "storage_type": "hash"
    },
    "fields": [
        {
            "name": "content",
            "type": "text"
        },
        {
            "name": "embedding",
            "type": "vector",
            "attrs": {
                "dims": 1536,  # OpenAI ada-002 dimensions
                "distance_metric": "cosine",
                "algorithm": "flat"  # or "hnsw" for large datasets
            }
        },
        {
            "name": "source",
            "type": "tag"
        },
        {
            "name": "created_at",
            "type": "numeric"
        }
    ]
}

# Create index
index = SearchIndex.from_dict(schema)
index.connect("redis://localhost:6379")
index.create(overwrite=True)

# Add documents
documents = [
    {
        "content": "Redis 8 introduces LangCache for semantic caching, reducing LLM costs by 70-90%",
        "source": "redis-blog",
        "created_at": 1730000000
    },
    {
        "content": "RedisVL provides vector search with sub-millisecond latency for AI applications",
        "source": "docs",
        "created_at": 1730000001
    },
    {
        "content": "LangGraph integrates with Redis for persistent agent memory across sessions",
        "source": "langchain-docs",
        "created_at": 1730000002
    }
]

# Generate embeddings and store
for i, doc in enumerate(documents):
    doc["embedding"] = get_embedding(doc["content"])
    index.load([doc], keys=[f"doc:{i}"])

# Perform vector search
query_text = "How to reduce costs for LLM applications?"
query_embedding = get_embedding(query_text)

query = VectorQuery(
    vector=query_embedding,
    vector_field_name="embedding",
    return_fields=["content", "source", "created_at"],
    num_results=3
)

results = index.query(query)

print(f"Query: {query_text}\n")
print("Top Results:")
for i, result in enumerate(results, 1):
    print(f"{i}. [{result['source']}] {result['content']}")
    print(f"   Score: {result['vector_distance']:.4f}\n")

# Output:
# Query: How to reduce costs for LLM applications?
#
# Top Results:
# 1. [redis-blog] Redis 8 introduces LangCache for semantic caching, reducing LLM costs by 70-90%
#    Score: 0.1234
#
# 2. [docs] RedisVL provides vector search with sub-millisecond latency for AI applications
#    Score: 0.2456
```

### Production RAG System with RedisVL

```python
from redisvl.index import SearchIndex
from redisvl.query import VectorQuery
from openai import OpenAI
from typing import List, Dict
import hashlib

class RedisRAGSystem:
    def __init__(self, redis_url: str = "redis://localhost:6379"):
        self.client = OpenAI()
        self.redis_url = redis_url

        # Create vector index
        schema = {
            "index": {
                "name": "knowledge_base",
                "prefix": "kb",
                "storage_type": "hash"
            },
            "fields": [
                {"name": "content", "type": "text"},
                {"name": "title", "type": "text"},
                {"name": "embedding", "type": "vector", "attrs": {
                    "dims": 1536,
                    "distance_metric": "cosine",
                    "algorithm": "hnsw",  # Faster for large datasets
                    "m": 16,
                    "ef_construction": 200
                }},
                {"name": "category", "type": "tag"},
                {"name": "timestamp", "type": "numeric"}
            ]
        }

        self.index = SearchIndex.from_dict(schema)
        self.index.connect(redis_url)
        self.index.create(overwrite=True)

    def _get_embedding(self, text: str) -> List[float]:
        """Generate embedding"""
        response = self.client.embeddings.create(
            model="text-embedding-ada-002",
            input=text
        )
        return response.data[0].embedding

    def add_document(self, content: str, title: str, category: str):
        """Add document to knowledge base"""
        import time

        doc_id = hashlib.md5(content.encode()).hexdigest()

        doc = {
            "content": content,
            "title": title,
            "category": category,
            "embedding": self._get_embedding(content),
            "timestamp": int(time.time())
        }

        self.index.load([doc], keys=[f"kb:{doc_id}"])
        print(f"✅ Added document: {title}")

    def retrieve(self, query: str, top_k: int = 3) -> List[Dict]:
        """Retrieve relevant documents"""
        query_embedding = self._get_embedding(query)

        vector_query = VectorQuery(
            vector=query_embedding,
            vector_field_name="embedding",
            return_fields=["content", "title", "category"],
            num_results=top_k
        )

        results = self.index.query(vector_query)
        return results

    def generate_answer(self, query: str, top_k: int = 3) -> Dict:
        """RAG: Retrieve + Generate"""

        # 1. Retrieve relevant docs
        docs = self.retrieve(query, top_k)

        if not docs:
            return {
                "answer": "I don't have enough information to answer that.",
                "sources": []
            }

        # 2. Build context from retrieved docs
        context = "\n\n".join([
            f"[{doc['title']}]\n{doc['content']}"
            for doc in docs
        ])

        # 3. Generate answer with LLM
        response = self.client.chat.completions.create(
            model="gpt-4",
            messages=[
                {
                    "role": "system",
                    "content": "You are a helpful assistant. Answer questions based on the provided context. If the context doesn't contain relevant information, say so."
                },
                {
                    "role": "user",
                    "content": f"Context:\n{context}\n\nQuestion: {query}\n\nAnswer:"
                }
            ],
            temperature=0.7,
            max_tokens=500
        )

        answer = response.choices[0].message.content

        return {
            "answer": answer,
            "sources": [{"title": doc["title"], "category": doc["category"]} for doc in docs]
        }

# Usage
rag = RedisRAGSystem()

# Add knowledge base
rag.add_document(
    content="Redis 8 introduces LangCache, a semantic caching service that reduces LLM costs by 70-90% by caching similar queries.",
    title="Redis 8 LangCache",
    category="features"
)

rag.add_document(
    content="RedisVL is a Python library for vector search, providing sub-millisecond latency for similarity search in AI applications.",
    title="RedisVL Overview",
    category="tools"
)

rag.add_document(
    content="Redis supports three types of agent memory: short-term (session context), long-term (vector embeddings), and structured (user profiles).",
    title="Agent Memory Types",
    category="concepts"
)

# Ask question
result = rag.generate_answer("How can I reduce my LLM costs?")

print(f"Question: How can I reduce my LLM costs?\n")
print(f"Answer: {result['answer']}\n")
print(f"Sources: {', '.join([s['title'] for s in result['sources']])}")
```

---

## 🧠 Agent Memory Management

Redis excels at managing all three types of agent memory with **<1ms latency**.

### Short-Term Memory (Conversation Context)

```python
import redis
import json
from datetime import datetime, timedelta

class ShortTermMemory:
    """Manage agent's short-term (working) memory"""

    def __init__(self, redis_client: redis.Redis):
        self.redis = redis_client

    def store_message(
        self,
        session_id: str,
        role: str,  # "user" or "assistant"
        content: str,
        ttl_hours: int = 24
    ):
        """Store conversation message"""
        key = f"session:{session_id}:messages"

        message = {
            "role": role,
            "content": content,
            "timestamp": datetime.now().isoformat()
        }

        # Add to list
        self.redis.rpush(key, json.dumps(message))

        # Set expiry (auto-cleanup old sessions)
        self.redis.expire(key, timedelta(hours=ttl_hours))

    def get_conversation_history(
        self,
        session_id: str,
        last_n: int = 10
    ) -> list:
        """Retrieve recent conversation history"""
        key = f"session:{session_id}:messages"

        # Get last N messages
        messages_raw = self.redis.lrange(key, -last_n, -1)

        messages = [json.loads(msg) for msg in messages_raw]
        return messages

    def get_context_for_llm(self, session_id: str, max_messages: int = 10) -> list:
        """Format conversation history for LLM"""
        messages = self.get_conversation_history(session_id, max_messages)

        # Convert to LLM format
        return [
            {"role": msg["role"], "content": msg["content"]}
            for msg in messages
        ]

    def clear_session(self, session_id: str):
        """Clear session memory"""
        key = f"session:{session_id}:messages"
        self.redis.delete(key)

# Usage
r = redis.Redis(host='localhost', port=6379, decode_responses=True)
memory = ShortTermMemory(r)

session_id = "user_123_session_abc"

# Simulate conversation
memory.store_message(session_id, "user", "What is Redis?")
memory.store_message(session_id, "assistant", "Redis is an in-memory data store...")

memory.store_message(session_id, "user", "How fast is it?")
memory.store_message(session_id, "assistant", "Redis provides sub-millisecond latency...")

# Get context for next LLM call
context = memory.get_context_for_llm(session_id)
print(context)
# [
#   {"role": "user", "content": "What is Redis?"},
#   {"role": "assistant", "content": "Redis is an in-memory data store..."},
#   {"role": "user", "content": "How fast is it?"},
#   {"role": "assistant", "content": "Redis provides sub-millisecond latency..."}
# ]
```

### Long-Term Memory (Semantic Search)

```python
from redisvl.index import SearchIndex
from redisvl.query import VectorQuery
from openai import OpenAI
import hashlib
from datetime import datetime

class LongTermMemory:
    """Manage agent's long-term semantic memory"""

    def __init__(self, user_id: str, redis_url: str = "redis://localhost:6379"):
        self.user_id = user_id
        self.client = OpenAI()

        # Create user-specific vector index
        schema = {
            "index": {
                "name": f"memory_{user_id}",
                "prefix": f"mem:{user_id}",
                "storage_type": "hash"
            },
            "fields": [
                {"name": "content", "type": "text"},
                {"name": "memory_type", "type": "tag"},  # "fact", "preference", "experience"
                {"name": "embedding", "type": "vector", "attrs": {
                    "dims": 1536,
                    "distance_metric": "cosine",
                    "algorithm": "hnsw"
                }},
                {"name": "timestamp", "type": "numeric"},
                {"name": "importance", "type": "numeric"}  # 1-10 scale
            ]
        }

        self.index = SearchIndex.from_dict(schema)
        self.index.connect(redis_url)
        self.index.create(overwrite=True)

    def _get_embedding(self, text: str) -> list:
        """Generate embedding"""
        response = self.client.embeddings.create(
            model="text-embedding-ada-002",
            input=text
        )
        return response.data[0].embedding

    def store_memory(
        self,
        content: str,
        memory_type: str = "experience",
        importance: int = 5
    ):
        """Store long-term memory"""
        memory_id = hashlib.md5(
            f"{content}{datetime.now().isoformat()}".encode()
        ).hexdigest()

        memory = {
            "content": content,
            "memory_type": memory_type,
            "embedding": self._get_embedding(content),
            "timestamp": int(datetime.now().timestamp()),
            "importance": importance
        }

        self.index.load([memory], keys=[f"mem:{self.user_id}:{memory_id}"])

    def recall(self, query: str, top_k: int = 5) -> list:
        """Recall relevant memories"""
        query_embedding = self._get_embedding(query)

        vector_query = VectorQuery(
            vector=query_embedding,
            vector_field_name="embedding",
            return_fields=["content", "memory_type", "importance", "timestamp"],
            num_results=top_k
        )

        results = self.index.query(vector_query)
        return results

# Usage
ltm = LongTermMemory(user_id="user_123")

# Store memories
ltm.store_memory(
    "User prefers Python over JavaScript for backend development",
    memory_type="preference",
    importance=8
)

ltm.store_memory(
    "User successfully deployed a microservices architecture using Docker and Kubernetes",
    memory_type="experience",
    importance=9
)

ltm.store_memory(
    "User's tech stack: FastAPI, PostgreSQL, Redis, React",
    memory_type="fact",
    importance=7
)

# Recall relevant memories
memories = ltm.recall("What programming languages does the user like?")

print("Recalled Memories:")
for mem in memories:
    print(f"- [{mem['memory_type']}] {mem['content']}")
    print(f"  Relevance: {1 - float(mem['vector_distance']):.2%}\n")
```

### Structured Memory (User Profiles & State)

```python
import redis
import json

class StructuredMemory:
    """Manage agent's structured memory (facts, profiles, state)"""

    def __init__(self, redis_client: redis.Redis):
        self.redis = redis_client

    def store_user_profile(self, user_id: str, profile: dict):
        """Store user profile"""
        key = f"profile:{user_id}"
        self.redis.hset(key, mapping={
            k: json.dumps(v) if isinstance(v, (dict, list)) else str(v)
            for k, v in profile.items()
        })

    def get_user_profile(self, user_id: str) -> dict:
        """Get user profile"""
        key = f"profile:{user_id}"
        data = self.redis.hgetall(key)

        # Decode values
        profile = {}
        for k, v in data.items():
            try:
                profile[k] = json.loads(v)
            except:
                profile[k] = v

        return profile

    def update_preference(self, user_id: str, pref_key: str, value):
        """Update specific preference"""
        key = f"profile:{user_id}"
        self.redis.hset(key, pref_key, json.dumps(value))

    def store_agent_state(self, agent_id: str, state: dict):
        """Store agent state"""
        key = f"agent_state:{agent_id}"
        self.redis.set(key, json.dumps(state), ex=3600)  # 1 hour TTL

    def get_agent_state(self, agent_id: str) -> dict:
        """Get agent state"""
        key = f"agent_state:{agent_id}"
        data = self.redis.get(key)
        return json.loads(data) if data else {}

# Usage
r = redis.Redis(host='localhost', port=6379, decode_responses=True)
memory = StructuredMemory(r)

# Store user profile
memory.store_user_profile("user_123", {
    "name": "Alice",
    "email": "alice@example.com",
    "preferences": {
        "language": "Python",
        "theme": "dark",
        "notifications": True
    },
    "subscription_tier": "premium",
    "tech_interests": ["AI", "DevOps", "Cloud"]
})

# Update specific preference
memory.update_preference("user_123", "preferences", {
    "language": "Python",
    "theme": "light",  # Changed
    "notifications": True
})

# Get profile
profile = memory.get_user_profile("user_123")
print(f"User: {profile['name']}")
print(f"Interests: {', '.join(profile['tech_interests'])}")

# Store agent state
memory.store_agent_state("agent_search_001", {
    "current_task": "researching Redis AI features",
    "progress": 0.75,
    "partial_results": ["LangCache", "RedisVL", "Agent Memory Server"]
})
```

---

## 🦜 LangChain & LangGraph Integration

### LangChain with Redis Vector Store

```python
from langchain_openai import OpenAIEmbeddings, ChatOpenAI
from langchain_redis import RedisVectorStore
from langchain.text_splitter import RecursiveCharacterTextSplitter
from langchain.chains import RetrievalQA

# Initialize embeddings
embeddings = OpenAIEmbeddings(model="text-embedding-ada-002")

# Create Redis vector store
vector_store = RedisVectorStore(
    redis_url="redis://localhost:6379",
    index_name="langchain_docs",
    embedding=embeddings
)

# Add documents
documents = [
    "Redis 8 introduces LangCache for semantic caching of LLM responses.",
    "RedisVL provides vector search capabilities with sub-millisecond latency.",
    "LangGraph integrates with Redis for persistent agent memory.",
]

vector_store.add_texts(documents)

# Create retrieval chain
llm = ChatOpenAI(model="gpt-4", temperature=0)

qa_chain = RetrievalQA.from_chain_type(
    llm=llm,
    chain_type="stuff",
    retriever=vector_store.as_retriever(search_kwargs={"k": 3})
)

# Query
question = "How does Redis help with LLM costs?"
answer = qa_chain.invoke({"query": question})

print(f"Q: {question}")
print(f"A: {answer['result']}")
```

### LangGraph with Redis Checkpointing

```python
from langgraph.checkpoint.redis import RedisSaver
from langgraph.graph import StateGraph, END
from typing import TypedDict, Annotated
import operator

# Define state
class AgentState(TypedDict):
    messages: Annotated[list, operator.add]
    counter: int

# Create graph
workflow = StateGraph(AgentState)

def process_node(state: AgentState):
    """Process messages"""
    return {
        "messages": [f"Processed: {state['messages'][-1]}"],
        "counter": state["counter"] + 1
    }

workflow.add_node("process", process_node)
workflow.set_entry_point("process")
workflow.add_edge("process", END)

# Initialize Redis checkpointer
checkpointer = RedisSaver.from_conn_info(
    host="localhost",
    port=6379,
    db=0
)

# Compile with persistence
app = workflow.compile(checkpointer=checkpointer)

# Run with thread_id for persistence
config = {"configurable": {"thread_id": "conversation_123"}}

# First run
result1 = app.invoke(
    {"messages": ["Hello"], "counter": 0},
    config=config
)
print(f"Run 1: {result1}")

# Second run - resumes from checkpoint
result2 = app.invoke(
    {"messages": ["World"], "counter": result1["counter"]},
    config=config
)
print(f"Run 2: {result2}")

# Agent memory persists across sessions!
```

---

## 🤝 AutoGen & CrewAI Integration

### AutoGen with Redis Caching

```python
import autogen
from autogen import AssistantAgent, UserProxyAgent

# Configure LLM with Redis caching
llm_config = {
    "cache_seed": 42,
    "config_list": [{
        "model": "gpt-4",
        "api_key": "your-api-key"
    }],
    "cache": {
        "type": "redis",
        "redis_url": "redis://localhost:6379",
        "ttl": 3600
    }
}

# Create assistant agent
assistant = AssistantAgent(
    name="assistant",
    llm_config=llm_config,
    system_message="You are a helpful AI assistant."
)

# Create user proxy
user_proxy = UserProxyAgent(
    name="user_proxy",
    human_input_mode="NEVER",
    max_consecutive_auto_reply=5,
    code_execution_config={"work_dir": "coding"}
)

# Chat with caching
# First call - cache miss
user_proxy.initiate_chat(
    assistant,
    message="Explain Redis vector search"
)

# Similar call - cache hit (instant response)
user_proxy.initiate_chat(
    assistant,
    message="Tell me about Redis vector database"
)
```

### CrewAI with Redis State Management

```python
from crewai import Agent, Task, Crew
import redis
import json

# Initialize Redis
r = redis.Redis(host='localhost', port=6379, decode_responses=True)

# Define agents
researcher = Agent(
    role="Researcher",
    goal="Research AI and Redis integration",
    backstory="Expert in AI infrastructure and databases",
    verbose=True
)

writer = Agent(
    role="Writer",
    goal="Write comprehensive documentation",
    backstory="Technical writer specializing in AI/ML",
    verbose=True
)

# Define tasks
research_task = Task(
    description="Research Redis AI features including LangCache and RedisVL",
    agent=researcher,
    expected_output="Detailed research report"
)

writing_task = Task(
    description="Write a guide based on research findings",
    agent=writer,
    expected_output="Complete guide document"
)

# Create crew
crew = Crew(
    agents=[researcher, writer],
    tasks=[research_task, writing_task],
    verbose=True
)

# Store crew state in Redis
def save_crew_state(crew_id: str, state: dict):
    r.set(f"crew:{crew_id}:state", json.dumps(state), ex=3600)

def load_crew_state(crew_id: str) -> dict:
    data = r.get(f"crew:{crew_id}:state")
    return json.loads(data) if data else {}

# Run crew
crew_id = "crew_001"
result = crew.kickoff()

# Save final state
save_crew_state(crew_id, {
    "status": "completed",
    "result": result,
    "agents_used": ["researcher", "writer"]
})
```

---

## 🔄 Redis Streams for Event-Driven Agents

Redis Streams enable event-driven multi-agent architectures with guaranteed message delivery.

### Multi-Agent Coordination with Streams

```python
import redis
import json
import time
from threading import Thread

class AgentCoordinator:
    """Coordinate multiple agents via Redis Streams"""

    def __init__(self, redis_client: redis.Redis):
        self.redis = redis_client
        self.stream_name = "agent_events"

        # Create consumer groups
        try:
            self.redis.xgroup_create(
                self.stream_name,
                "agents",
                id='0',
                mkstream=True
            )
        except redis.ResponseError:
            pass  # Group already exists

    def dispatch_task(self, task_type: str, data: dict):
        """Dispatch task to agent stream"""
        event = {
            "task_type": task_type,
            "data": json.dumps(data),
            "timestamp": time.time()
        }

        message_id = self.redis.xadd(
            self.stream_name,
            event,
            maxlen=10000  # Keep last 10K events
        )

        print(f"📤 Dispatched task {task_type}: {message_id}")
        return message_id

    def process_events(self, agent_name: str, handler_fn):
        """Process events for specific agent"""
        print(f"🤖 Agent '{agent_name}' started listening...")

        while True:
            # Read from stream
            messages = self.redis.xreadgroup(
                "agents",
                agent_name,
                {self.stream_name: '>'},
                count=10,
                block=1000  # Block for 1 second
            )

            for stream, events in messages:
                for event_id, data in events:
                    try:
                        task_type = data[b'task_type'].decode()
                        task_data = json.loads(data[b'data'].decode())

                        print(f"✅ Agent '{agent_name}' processing: {task_type}")

                        # Process event
                        result = handler_fn(task_type, task_data)

                        # Acknowledge
                        self.redis.xack(self.stream_name, "agents", event_id)

                        # Publish result
                        self.publish_result(agent_name, task_type, result)

                    except Exception as e:
                        print(f"❌ Error processing event: {e}")

    def publish_result(self, agent_name: str, task_type: str, result: dict):
        """Publish agent result"""
        self.redis.xadd(
            "agent_results",
            {
                "agent": agent_name,
                "task_type": task_type,
                "result": json.dumps(result),
                "timestamp": time.time()
            },
            maxlen=10000
        )

# Usage
r = redis.Redis(host='localhost', port=6379)
coordinator = AgentCoordinator(r)

# Define agent handlers
def search_agent_handler(task_type: str, data: dict):
    """Search agent"""
    if task_type == "search":
        # Simulate search
        time.sleep(0.5)
        return {"results": [f"Result for '{data['query']}'"]}
    return {}

def analysis_agent_handler(task_type: str, data: dict):
    """Analysis agent"""
    if task_type == "analyze":
        # Simulate analysis
        time.sleep(0.7)
        return {"analysis": f"Analysis of {data['text'][:50]}..."}
    return {}

# Start agents in separate threads
Thread(
    target=coordinator.process_events,
    args=("search_agent", search_agent_handler),
    daemon=True
).start()

Thread(
    target=coordinator.process_events,
    args=("analysis_agent", analysis_agent_handler),
    daemon=True
).start()

# Dispatch tasks
coordinator.dispatch_task("search", {"query": "Redis AI features"})
coordinator.dispatch_task("analyze", {"text": "Redis 8 introduces new capabilities..."})

# Keep running
time.sleep(5)
```

---

## 📚 Production Case Studies

### Raymond James - Financial Services Chatbot

**Challenge:** Take prototype chatbot to production with high accuracy and performance

**Solution:**
- Redis for ultra-low latency response caching
- RedisVL for semantic search across financial documents
- A/B testing insights to improve UX

**Results:**
- ✅ Sub-100ms response times
- ✅ Validated accuracy improvements
- ✅ Production-ready scalability

### Amgen - Scientific Document Analysis

**Challenge:** Scan and summarize millions of scientific and clinical documents

**Solution:**
- Redis vector database for embedding storage
- Semantic search across research papers
- AI agents with persistent memory

**Results:**
- ✅ Millions of documents indexed
- ✅ Fast similarity search (<10ms)
- ✅ Improved research workflows

---

## ✅ Best Practices

### 1. Memory Hierarchy

```python
# ✅ DO: Use appropriate memory type for each use case
short_term = Redis Strings/Lists  # Conversation context
long_term = RedisVL (Vectors)     # Semantic recall
structured = Redis Hashes/JSON    # User profiles

# ❌ DON'T: Use vectors for everything (expensive embeddings)
```

### 2. Cache Strategy

```python
# ✅ DO: Use LangCache for expensive LLM calls
cache_threshold = 0.1  # Similarity threshold

# ❌ DON'T: Cache everything (storage costs)
# Only cache frequently asked questions
```

### 3. TTL Management

```python
# ✅ DO: Set appropriate TTLs
session_context: 24 hours
semantic_cache: 7 days
user_profiles: No expiry

# ❌ DON'T: Store everything permanently
```

### 4. Connection Pooling

```python
# ✅ DO: Use connection pools
pool = redis.ConnectionPool(
    host='localhost',
    port=6379,
    max_connections=50
)
r = redis.Redis(connection_pool=pool)

# ❌ DON'T: Create new connections for each request
```

---

## 🎯 Example Applications

### Complete AI Agent with All Memory Types

```python
from openai import OpenAI
import redis
from redisvl.index import SearchIndex
from redisvl.query import VectorQuery
import json
from typing import Dict, List

class IntelligentAgent:
    """Production AI agent with Redis-powered memory"""

    def __init__(self, user_id: str):
        self.user_id = user_id
        self.client = OpenAI()
        self.redis = redis.Redis(host='localhost', port=6379, decode_responses=True)

        # Initialize all three memory types
        self._init_short_term_memory()
        self._init_long_term_memory()
        self._init_structured_memory()

    def _init_short_term_memory(self):
        """Session context"""
        self.session_key = f"session:{self.user_id}:current"

    def _init_long_term_memory(self):
        """Vector memory for semantic recall"""
        schema = {
            "index": {"name": f"ltm_{self.user_id}", "prefix": f"ltm:{self.user_id}"},
            "fields": [
                {"name": "content", "type": "text"},
                {"name": "embedding", "type": "vector", "attrs": {
                    "dims": 1536, "distance_metric": "cosine", "algorithm": "hnsw"
                }}
            ]
        }
        self.ltm_index = SearchIndex.from_dict(schema)
        self.ltm_index.connect("redis://localhost:6379")
        self.ltm_index.create(overwrite=False)

    def _init_structured_memory(self):
        """User profile and preferences"""
        self.profile_key = f"profile:{self.user_id}"

    def chat(self, user_message: str) -> str:
        """Process user message with full memory context"""

        # 1. Add to short-term memory
        self.redis.rpush(f"{self.session_key}:messages", json.dumps({
            "role": "user",
            "content": user_message
        }))

        # 2. Retrieve relevant long-term memories
        relevant_memories = self._recall_memories(user_message, top_k=3)

        # 3. Get user profile
        profile = self.redis.hgetall(self.profile_key)

        # 4. Build context
        recent_messages = [
            json.loads(msg)
            for msg in self.redis.lrange(f"{self.session_key}:messages", -10, -1)
        ]

        # 5. Generate response with LLM
        system_prompt = f"""You are a helpful assistant.

User Profile: {profile.get('name', 'Unknown')}
Preferences: {profile.get('preferences', 'None')}

Relevant Memories:
{chr(10).join(f"- {mem['content']}" for mem in relevant_memories)}

Use this context to provide personalized responses."""

        response = self.client.chat.completions.create(
            model="gpt-4",
            messages=[
                {"role": "system", "content": system_prompt},
                *recent_messages
            ]
        )

        answer = response.choices[0].message.content

        # 6. Store response in short-term memory
        self.redis.rpush(f"{self.session_key}:messages", json.dumps({
            "role": "assistant",
            "content": answer
        }))

        # 7. Store important info in long-term memory
        self._store_memory(f"User asked: {user_message}. Response: {answer[:200]}")

        return answer

    def _recall_memories(self, query: str, top_k: int = 3) -> List[Dict]:
        """Retrieve relevant long-term memories"""
        query_embedding = self._get_embedding(query)

        vector_query = VectorQuery(
            vector=query_embedding,
            vector_field_name="embedding",
            return_fields=["content"],
            num_results=top_k
        )

        try:
            results = self.ltm_index.query(vector_query)
            return results
        except:
            return []

    def _store_memory(self, content: str):
        """Store in long-term memory"""
        import hashlib
        memory_id = hashlib.md5(content.encode()).hexdigest()

        memory = {
            "content": content,
            "embedding": self._get_embedding(content)
        }

        self.ltm_index.load([memory], keys=[f"ltm:{self.user_id}:{memory_id}"])

    def _get_embedding(self, text: str) -> List[float]:
        """Generate embedding"""
        response = self.client.embeddings.create(
            model="text-embedding-ada-002",
            input=text
        )
        return response.data[0].embedding

    def update_profile(self, **kwargs):
        """Update user profile (structured memory)"""
        for key, value in kwargs.items():
            self.redis.hset(self.profile_key, key, str(value))

# Usage
agent = IntelligentAgent(user_id="alice_123")

# Set user profile
agent.update_profile(
    name="Alice",
    preferences="Prefers Python, likes detailed explanations"
)

# Chat with full memory context
response1 = agent.chat("What is Redis?")
print(f"Agent: {response1}\n")

response2 = agent.chat("How does it compare to PostgreSQL?")
print(f"Agent: {response2}\n")

# Agent remembers context and preferences!
response3 = agent.chat("Can you give me a Python example?")
print(f"Agent: {response3}")
```

---

## 🎓 Summary

Redis has become the **leading infrastructure** for production AI agent systems in 2025:

✅ **Ultra-Low Latency** - <1ms for all memory operations
✅ **Complete Memory Solution** - All 3 types (short, long, structured)
✅ **Cost Optimization** - 70-90% savings with LangCache
✅ **Vector Search** - RedisVL for semantic similarity
✅ **Production Scale** - 1M+ operations/second
✅ **Framework Integration** - LangChain, LangGraph, AutoGen, CrewAI
✅ **Developer Adoption** - 43% of developers use Redis for agents

**Next Steps:**
1. [Explore Redis Basics →](REDIS.md)
2. [Compare with Kafka AI Agents →](KAFKA-AI-AGENTS.md)
3. [Compare with RabbitMQ AI Agents →](AI-AGENTS.md)

---

<div align="center">

**⭐ Star this repo if you found it helpful!**

[🏠 Back to Main](../README.md) | [📖 Redis Guide](README.md)

</div>
