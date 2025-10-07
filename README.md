# wikimedia-opensearch-kafka
Streams live Wikimedia data through Kafka and stores it in OpenSearch for real-time search and analytics.

A multi-module Java project demonstrating real-time streaming with **Apache Kafka**.
The producer streams live Wikimedia changes into Kafka, and the consumer reads those messages and indexes them into **OpenSearch**.

---

## Modules

| Module                        | Description                                                                                |
| ----------------------------- | ------------------------------------------------------------------------------------------ |
| **kafka-producer-wikimedia**  | Connects to the Wikimedia Event Stream API and publishes real-time edits to a Kafka topic. |
| **kafka-consumer-opensearch** | Consumes events from Kafka and stores them in OpenSearch for searching and visualization.  |

---

## Tech Stack
- **Java**
- **Docker**
- **Kafka**
- **OpenSearch**
  
---

##  Infrastructure

This project includes two Docker Compose configurations:

### **1. Kafka stack**

Located at `docker-compose.kafka.yml`

Services:

* **Zookeeper** (manages Kafka brokers)
* **Kafka Broker** (message broker)
* **Schema Registry** (optional for Avro or JSON schemas)

---

### **2. OpenSearch stack**

Located at `docker-compose.opensearch.yml`

Services:

* **OpenSearch** (Elasticsearch-compatible search engine)
* **OpenSearch Dashboards** (visualization interface)

---

## Environment Variables

To be able to stream read configuration from a `.env` file in the project root.

### Example `.env`

```
USER_AGENT=your_github_account_url

```
---

## Running this project locally

Before running the producer and consumer, start the required services:

```
-> docker compose -f docker-compose.opensearch.yml -f docker-compose.kafka.yml up -d

```

Once running, services will be available on:

**Kafka** → http://localhost:9092

**OpenSearch** → http://localhost:9200

**Dashboards** → http://localhost:5601

### Linux / macOS

```bash
./run.sh
```

### Windows

```bash
run.bat
```

These scripts start:

**The producer (kafka-producer-wikimedia)**

**The consumer (kafka-consumer-opensearch)**

Both modules will keep running and streaming data in real time.

## Visualizing Data

Once messages are flowing:

1. Go to **OpenSearch Dashboards** → [http://localhost:5601](http://localhost:5601)
2. Create an index pattern for your topic’s index (e.g. `wikimedia*`)
3. Explore real-time edits in Discover or visualize them.
