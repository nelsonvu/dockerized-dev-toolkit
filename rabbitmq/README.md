# Docker Toolkit: Setting Up RabbitMQ

## Installation

```bash
# Create an .env file based on the provided .env.example file
cp .env.example .env

# Create folders to store RabbitMQ data and log
mkdir data log

# Run RabbitMQ container
docker-compose up -d
```

## Result

The RabbitMQ service is running on port 5672

The HTTP management UI is running on port 15672
