
<div align="center">
  <img src="https://picsum.photos/seed/sentinel-logo/150/150" alt="Sentinel Logo" />
  <h1>Sentinel: Real-Time Trend Detection Engine</h1>
  <p>
    A high-performance dashboard for real-time social media and news trend detection, sentiment analysis, and viral event alerting.
  </p>
  <p>
    <img src="https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB" alt="React" />
    <img src="https://img.shields.io/badge/TypeScript-007ACC?style=for-the-badge&logo=typescript&logoColor=white" alt="TypeScript" />
    <img src="https://img.shields.io/badge/Tailwind_CSS-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white" alt="Tailwind CSS" />
    <img src="https://img.shields.io/badge/Kafka-231F20?style=for-the-badge&logo=apache-kafka&logoColor=white" alt="Apache Kafka" />
    <img src="https://img.shields.io/badge/Apache_Flink-E6526F?style=for-the-badge&logo=apache-flink&logoColor=white" alt="Apache Flink" />
    <img src="https://img.shields.io/badge/Elasticsearch-005571?style=for-the-badge&logo=elasticsearch&logoColor=white" alt="Elasticsearch" />
  </p>
</div>

---

## 🌟 Introduction

In today's fast-paced digital world, missing an emerging trend or a brewing PR crisis can cost millions. **Sentinel** is a powerful, real-time intelligence platform designed to monitor the digital pulse of social media and news outlets. It identifies nascent trends, tracks sentiment shifts, and alerts stakeholders to significant events, enabling proactive and data-driven decision-making.

This project showcases a scalable, resilient system architecture capable of processing high-volume data streams, making it a perfect example of a modern data-intensive application suitable for FAANG-level engineering challenges.

## ✨ Key Features (Phase 1)

- **Real-Time Data Streaming**: Simulates a live feed of posts from various sources like Twitter, Reddit, and News articles.
- **Trend & Keyword Detection**: Identifies and visualizes spikes in keyword and hashtag mentions.
- **Sentiment Analysis**: Tracks the overall sentiment (positive, neutral, negative) of the discourse over time.
- **Dynamic Dashboards**: A visually stunning and responsive UI with interactive charts and graphs for at-a-glance insights.
- **Automated Alerting**: Sends real-time alerts for "viral events," PR spikes, or significant shifts in public sentiment.

## 🖼️ Screenshots

<div align="center">
  <img src="/img/sentinel.png" alt="Dashboard Dark Mode" width="80%">
  <p><em>Sentinel's primary dashboard in dark mode.</em></p>
</div>

## 🛠️ Tech Stack

This project is composed of a sophisticated backend for data processing and a modern frontend for visualization.

| Category              | Technology                                                                                                                                                                                          |
| --------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Frontend**          | [React](https://reactjs.org/), [TypeScript](https://www.typescriptlang.org/), [Tailwind CSS](https://tailwindcss.com/), [Recharts](https://recharts.org/)                                               |
| **Data Ingestion**    | [Apache Kafka](https://kafka.apache.org/)                                                                                                                                                           |
| **Stream Processing** | [Apache Flink](https://flink.apache.org/) or [Spark Streaming](https://spark.apache.org/streaming/)                                                                                                     |
| **Data Storage**      | [Elasticsearch](https://www.elastic.co/) (for search/analytics), [InfluxDB](https://www.influxdata.com/) (for time-series metrics)                                                                     |
| **Backend API**       | [Node.js](https://nodejs.org/) with [GraphQL](https://graphql.org/) / [gRPC](https://grpc.io/), [WebSockets](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API) for real-time updates |
| **Alerting**          | [Prometheus Alertmanager](https://prometheus.io/docs/alerting/latest/alertmanager/) or Flink CEP                                                                                                        |
| **Deployment**        | [Docker](https://www.docker.com/), [Kubernetes](https://kubernetes.io/), [AWS](https://aws.amazon.com/)/[GCP](https://cloud.google.com/)/[Azure](https://azure.microsoft.com/)                         |


## 🏗️ System Design & Architecture

The architecture is designed for scalability, low latency, and fault tolerance, handling massive volumes of data in real time.

<div align="center">
  <img src="/img/architecture.jpeg" alt="System Architecture Diagram">
  <p><em>High-Level System Architecture Diagram</em></p>
</div>

### 1. Data Ingestion Layer

- **Source Connectors**: Dedicated services connect to external APIs (e.g., Twitter/X API, Reddit API, NewsAPI). These connectors are responsible for fetching data and handling API rate limits and authentication.
- **Message Broker (Apache Kafka)**: All incoming data is published to Kafka topics (e.g., `twitter_posts`, `reddit_comments`). Kafka acts as a highly scalable, persistent buffer, decoupling the data producers from the consumers and ensuring data durability.

### 2. Real-Time Processing Layer

- **Stream Processor (Apache Flink)**: A Flink cluster consumes data from Kafka topics. Flink is chosen for its true streaming capabilities, low latency, and robust state management.
- **Processing Jobs**:
    - **Enrichment**: Raw data is parsed, cleaned, and enriched with metadata.
    - **Natural Language Processing (NLP)**: Keywords, entities, and hashtags are extracted.
    - **Sentiment Analysis**: A machine learning model (e.g., a pre-trained transformer model) is applied to assign a sentiment score to each piece of content.
    - **Aggregation**: Data is aggregated into time windows (e.g., 1-minute intervals) to calculate metrics like mention counts and average sentiment.
    - **Anomaly/Spike Detection**: Flink's Complex Event Processing (CEP) library or custom logic is used to detect sudden spikes in metrics, which triggers alerts.

### 3. Data Storage Layer

- **Search & Analytics (Elasticsearch)**: Processed and enriched posts are indexed in Elasticsearch. This allows for powerful, fast, full-text search and complex ad-hoc queries from the frontend.
- **Time-Series Database (InfluxDB)**: Aggregated metrics (mention counts per topic, average sentiment) are stored in a time-series database. This is highly optimized for storing and querying time-stamped data, which is ideal for powering the dashboard charts.
- **Raw Data Lake (S3)**: For compliance and historical analysis, raw, unprocessed data can be archived in a cost-effective object store like Amazon S3.

### 4. Backend & API Layer

- **API Service (Node.js/GraphQL)**: A backend service provides a GraphQL API for the frontend. This API queries Elasticsearch for post data and InfluxDB for chart metrics. GraphQL allows the frontend to request exactly the data it needs, reducing payload size.
- **Real-Time Push (WebSockets)**: A WebSocket server is used to push new posts, updated metrics, and alerts to connected clients in real-time, providing a live dashboard experience without constant polling.

### 5. Frontend (Presentation Layer)

- **Web Application (React)**: The user interface is a single-page application built with React and TypeScript. It provides an interactive and responsive dashboard for data visualization.
- **State Management**: Client-side state is managed to handle the influx of real-time data from WebSockets efficiently.
- **Visualization (Recharts)**: Interactive charts and graphs are used to visualize trends, sentiment, and other key metrics.

## 🚀 Getting Started

To run the frontend simulation locally:

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/your-username/sentinel.git
    cd sentinel
    ```

2.  **Install dependencies:**
    ```bash
    npm install
    ```

3.  **Set up environment variables:**
    Create a `.env` file and add your Gemini API key.
    ```
    API_KEY=YOUR_GEMINI_API_KEY
    ```

4.  **Run the development server:**
    ```bash
    npm run dev
    ```
    The application will be available at `http://localhost:3000`.

## 📄 License

This project is licensed under the MIT License. See the `LICENSE` file for details.

## Vedio Demo 

<video controls src="Social_media_feed.mp4" title="Sentinel" width="400"></video>