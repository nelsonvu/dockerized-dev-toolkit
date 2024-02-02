# Docker Toolkit: Setting Up MySQL

## Installation

```bash
# Create an .env file based on the provided .env.example file
cp .env.example .env

# Create folder to store MySQL data
mkdir data

# Run MySQL container
docker-compose up -d
```

## Result

Now, the MySQL service is running on port 3306
