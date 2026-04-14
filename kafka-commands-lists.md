# Kafka Commands Cheatsheet 🚀

## 🟢 Server

```bash
# Start Kafka server
kafka-server-start.bat C:\kafka\config\server.properties

# Stop Kafka server
kafka-server-stop.bat
```

---

## 📁 Topics

```bash
# Create topic
kafka-topics.bat --create --topic <TOPIC-NAME> --bootstrap-server localhost:9092 --partitions 1 --replication-factor 1

# List all topics
kafka-topics.bat --list --bootstrap-server localhost:9092

# Describe a topic (partitions, replicas, etc.)
kafka-topics.bat --describe --topic <TOPIC-NAME> --bootstrap-server localhost:9092

# Delete a topic
kafka-topics.bat --delete --topic <TOPIC-NAME> --bootstrap-server localhost:9092
```

---

## 📤 Producer

```bash
# Start producer (type message and press Enter to send)
kafka-console-producer.bat --topic <TOPIC-NAME> --bootstrap-server localhost:9092

# Producer with key
kafka-console-producer.bat --topic <TOPIC-NAME> --bootstrap-server localhost:9092 --property "parse.key=true" --property "key.separator=:"
```

---

## 📥 Consumer

```bash
# Read only new messages (live)
kafka-console-consumer.bat --topic <TOPIC-NAME> --bootstrap-server localhost:9092

# Read ALL messages from beginning
kafka-console-consumer.bat --topic <TOPIC-NAME> --bootstrap-server localhost:9092 --from-beginning

# Read with consumer group
kafka-console-consumer.bat --topic <TOPIC-NAME> --bootstrap-server localhost:9092 --group <GROUP-NAME> --from-beginning

# Read with key displayed
kafka-console-consumer.bat --topic <TOPIC-NAME> --bootstrap-server localhost:9092 --from-beginning --property print.key=true --property key.separator=" : "
```

---

## 👥 Consumer Groups

```bash
# List all consumer groups
kafka-consumer-groups.bat --list --bootstrap-server localhost:9092

# Describe a group (lag, offsets)
kafka-consumer-groups.bat --describe --group <GROUP-NAME> --bootstrap-server localhost:9092

# Reset offset to beginning
kafka-consumer-groups.bat --reset-offsets --to-earliest --group <GROUP-NAME> --topic <TOPIC-NAME> --bootstrap-server localhost:9092 --execute
```

---

## ⚙️ Storage (KRaft Mode)

```bash
# Generate cluster UUID
kafka-storage.bat random-uuid

# Format storage (first time only)
kafka-storage.bat format -t <UUID> -c C:\kafka\config\server.properties --standalone
```

---

## 🔍 Quick Tips

| Task | Command |
|------|---------|
| Check Kafka version | `kafka-topics.bat --version` |
| How many messages in topic | `kafka-run-class.bat kafka.tools.GetOffsetShell --topic <TOPIC> --bootstrap-server localhost:9092` |
| Increase partitions | `kafka-topics.bat --alter --topic <TOPIC> --partitions <N> --bootstrap-server localhost:9092` |
