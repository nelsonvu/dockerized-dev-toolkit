# Docker Toolkit: Setting Up MongoDB

## Installation

```bash
# Create an .env file based on the provided .env.example file
cp .env.example .env

# Create folder to store MongoDB data
mkdir data

# Run MongoDB container
docker-compose up -d
```

## Result

Now, the MongoDB service is running on port 27017
