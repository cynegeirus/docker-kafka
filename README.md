# 🚀 Kafka + Kafka UI (Docker Compose)

This repository contains a simple **Docker Compose** setup for running **Apache Kafka** along with **Kafka UI** for management and monitoring.  
It’s ideal for local development, testing, and experimenting with Kafka clusters.  

---

## 📦 Services

- **Kafka (Confluent 7.8.0)**
  - Port: `9092` (Client connections)
  - Port: `9093` (Controller connection)
  - Volume: `mq-data` → Persistent Kafka data
  - Hostname: `kafka.cynegeirus.local`

- **Kafka UI (Provectus)**
  - Port: `9091` (Web UI → http://localhost:9091)
  - Username / Password: `admin` / `YOUR_PASSWORD`
  - Hostname: `kafka-ui.cynegeirus.local`

---

## ⚙️ Setup

1. Clone the repository:
   ```bash
   git clone https://github.com/docker-kafka/kafka-docker.git
   cd docker-kafka
   ````

2. Update the `YOUR_IP_ADDRESS` in the `docker-compose.yml` file with your host machine’s IP address:

   ```yaml
   KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://192.168.1.100:9092
   KAFKA_CLUSTERS_0_BOOTSTRAPSERVERS: 192.168.1.100:9092
   ```

3. Start the services:

   ```bash
   docker compose up -d
   ```

4. Access Kafka UI:

   ```
   http://localhost:9091
   ```

---

## 🛠️ Example Usage

### Create a topic

```bash
docker exec -it kafka kafka-topics --create \
  --topic test-topic \
  --partitions 1 \
  --replication-factor 1 \
  --bootstrap-server localhost:9092
```

### List topics

```bash
docker exec -it kafka kafka-topics --list \
  --bootstrap-server localhost:9092
```

### Produce messages

```bash
docker exec -it kafka kafka-console-producer \
  --topic test-topic \
  --bootstrap-server localhost:9092
```

### Consume messages

```bash
docker exec -it kafka kafka-console-consumer \
  --topic test-topic \
  --from-beginning \
  --bootstrap-server localhost:9092
```

---

## 📝 Notes

* Replace `YOUR_IP_ADDRESS` with your actual machine IP (e.g., `192.168.1.100`).
* Kafka data is persisted in the `mq-data` Docker volume.
* Default credentials for Kafka UI are configurable via environment variables.

---

## 📜 License

This project is licensed under the [MIT License](LICENSE). See the license file for details.

---

## 🙌 Issues, Feature Requests or Support

Please use the Issue > New Issue button to submit issues, feature requests or support issues directly to me. You can also send an e-mail to akin.bicer@outlook.com.tr.
