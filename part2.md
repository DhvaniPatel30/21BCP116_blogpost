---
layout: part2
title: Part 2 - Setting Up the Backend Tier
permalink: /part2/
---

<!-- Content for Docker part 2 -->

# Part 2 - Setting Up the Backend Tier with Node.js

In this part of the tutorial, we will set up the backend tier using Node.js.

## Step 1: Dockerfile for Node.js Backend

```dockerfile
# Use the official Node.js image as the base image
FROM node:latest

# Set container name with roll number
ENV NODE_CONTAINER_NAME="21bcp116-backend"

# Create and set working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy backend source code
COPY . .

# Expose port 5000
EXPOSE 5000

# Command to run the backend server
CMD ["node", "server.js"]
```

![image](https://github.com/DhvaniPatel30/21BCP116_blogpost/assets/126047632/90445a05-cd0c-45e3-bcda-7418b683d463)


## Step 2: Building and Running Node.js Backend Container

``` dockerfile
# Build the Docker image for Node.js backend
docker build -t 21bcp116-backend .

# Run the Node.js backend container
docker run -d --name 21bcp116-backend -p 5000:5000 --network my-network 21bcp116-backend
```
![image](https://github.com/DhvaniPatel30/21BCP116_blogpost/assets/126047632/1f276ede-c67d-4873-aa2e-1d1b39d30303)

![image](https://github.com/DhvaniPatel30/21BCP116_blogpost/assets/126047632/29817b7e-ea7f-4cb5-836a-99c2efa989ae)
