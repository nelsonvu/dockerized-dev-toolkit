# Docker Toolkit: Setting Up Kafka

## Installation

```bash
# Create an .env file based on the provided .env.example file
cp .env.example .env

# Then, modify KAFKA_ADVERTISED_LISTENERS.EXTERNAL_DIFFERENT_HOST to your ip

# Create folder to store Kafka data
mkdir data

# Run Kafka container
docker-compose up -d
```

## Result

Now, the Kafka service is running on port 29092, 29093
