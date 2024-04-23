---
layout: part1
title: Part 1 - Setting Up the Database Tier
permalink: /part1/
---

<!-- Content for Docker part 1 -->

# Part 1 - Setting Up the Database Tier with MongoDB

In this part of the tutorial, we will set up the database tier using MongoDB.

## Step 1: Dockerfile for MongoDB

```dockerfile
# Use the official MongoDB image as the base image
FROM mongo:latest

# Set container name with roll number
ENV MONGO_CONTAINER_NAME="21bcp116-mongodb"
```

![Image](/images/Screenshot 2024-04-23 110138.png)

## Step 2: building and running the database

```dockerfile
# Build the Docker image for MongoDB
docker build -t 21bcp116-mongodb .

# Run the MongoDB container
docker run -d --name 21bcp116-mongodb -p 27017:27017 21bcp116-mongodb

```
![Image](/images/Screenshot 2024-04-23 114000.png)



## Step 3: Connecting MongoDB Container to Network
```dockerfile
# Create a Docker network
docker network create my-network

# Connect MongoDB container to the network
docker network connect my-network 21bcp116-mongodb
```

![Image](/images/Screenshot 2024-04-23 114134.png)

![Image](/images/Screenshot 2024-04-23 114256.png)