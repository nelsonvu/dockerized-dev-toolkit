# Docker Toolkit: Setting Up PostgreSQL

## Installation

```bash
# Create an .env file based on the provided .env.example file
cp .env.example .env

# Create folder to store PostgreSQL data
mkdir data

# Run PostgreSQL container
docker-compose up -d
```

## Result

Now, the PostgreSQL service is running on port 5432
