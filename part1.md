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
![image](https://github.com/DhvaniPatel30/21BCP116_blogpost/assets/126047632/7aa0593a-96fd-45c5-8904-0be8c752dfbd)

![image](https://github.com/DhvaniPatel30/21BCP116_blogpost/assets/126047632/d77a5e39-ee00-48d3-8ce3-72e3c6161a89)



## Step 2: building and running the database

```dockerfile
# Build the Docker image for MongoDB
docker build -t 21bcp116-mongodb .

# Run the MongoDB container
docker run -d --name 21bcp116-mongodb -p 27017:27017 21bcp116-mongodb

```
![image](https://github.com/DhvaniPatel30/21BCP116_blogpost/assets/126047632/1d397149-9509-4e7c-9df6-224ee797cee7)



## Step 3: Connecting MongoDB Container to Network
```dockerfile
# Create a Docker network
docker network create my-network

# Connect MongoDB container to the network
docker network connect my-network 21bcp116-mongodb
```

![image](https://github.com/DhvaniPatel30/21BCP116_blogpost/assets/126047632/c7ddb472-992f-48b9-a11e-61e08fffc6d4)
