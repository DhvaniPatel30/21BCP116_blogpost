# Docker and Three-Tier Architecture

## Introduction to Docker

Docker is a platform for developing, shipping, and running applications in containers. Containers allow developers to package an application with all of its dependencies into a standardized unit, ensuring that it will run consistently on any environment. Docker provides tools for building, deploying, and managing containers, making it easier to develop and deploy applications in various environments.

## What is Three-Tier Architecture?

Three-tier architecture is a software architecture pattern where an application is divided into three logical tiers or layers: the presentation tier, the application logic tier, and the data storage tier. Each tier has a specific role and responsibility:

1. **Presentation Tier (Frontend):** This tier is responsible for presenting information to the user and handling user interactions. It typically consists of user interfaces such as web browsers, mobile apps, or desktop applications.

2. **Application Logic Tier (Backend):** This tier contains the business logic of the application and is responsible for processing user requests, performing computations, and interacting with the data storage tier. It can include application servers, APIs, and microservices.

3. **Data Storage Tier (Database):** This tier stores and manages the data used by the application. It can be a relational database, NoSQL database, file system, or any other data storage solution.

## Using Docker in Three-Tier Architecture

Docker is particularly useful in implementing and deploying applications based on the three-tier architecture:

### 1. Database Tier

In the database tier, Docker can be used to containerize the database management system (DBMS) such as PostgreSQL, MySQL, or MongoDB. Docker containers provide a lightweight and portable way to run databases, ensuring consistency across different environments.

### 2. Backend Tier

For the backend tier, Docker containers can encapsulate the application logic, including the web servers, APIs, and microservices. Developers can package their backend code and dependencies into Docker images, making it easy to deploy and scale the application components independently.

### 3. Frontend Tier

In the frontend tier, Docker can be used to package and deploy the presentation layer components such as static web assets, JavaScript frameworks like React or Angular, and web servers like Nginx or Apache. Docker containers enable developers to build and deploy frontend applications with ease, ensuring consistency and reliability.

Folder Structure of project:
![image](https://github.com/DhvaniPatel30/21BCP116_blogpost/assets/126047632/b354f44c-be02-4dc4-beda-9451909a582a)




Folder structure of jenkyll:
![image](https://github.com/DhvaniPatel30/21BCP116_blogpost/assets/126047632/1fcbd2c4-c784-4111-8c8a-1d7c76ea1007)


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

---
layout: part3
title: Part 3 - Setting Up the Frontend Tier
permalink: /part3/
---

<!-- Content for Docker part 3 -->

# Part 3 - Setting Up the Frontend Tier with React

In this part of the tutorial, we will set up the frontend tier using React.

## Step 1: Dockerfile for React Frontend

```dockerfile
# Use the official Node.js image as the base image for building React app
FROM node:latest as build

# Set container name with roll number
ENV REACT_CONTAINER_NAME="21bcp116-frontend"

# Create and set working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy frontend source code
COPY . .

# Build React app
RUN npm run build

# Use NGINX for serving React app
FROM nginx:alpine

# Copy build files from build stage
COPY --from=build /app/build /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Command to start NGINX
CMD ["nginx", "-g", "daemon off;"]
```
![image](https://github.com/DhvaniPatel30/21BCP116_blogpost/assets/126047632/394edb19-b8b8-497e-b523-947099da4409)

## Step 2: Building and Running React Frontend Container
 ``` dockerfile
# Build the Docker image for React frontend
docker build -t 21bcp116-frontend .

# Run the React frontend container
docker run -d --name 21bcp116-frontend -p 80:80 --network my-network 21bcp116-frontend
```
![image](https://github.com/DhvaniPatel30/21BCP116_blogpost/assets/126047632/f35f7c53-bd46-46fe-95b2-a7eb77c43434)

![image](https://github.com/DhvaniPatel30/21BCP116_blogpost/assets/126047632/9a7aed04-5c19-48da-bdbc-7e15cb3c328e)


## Conclusion

Docker simplifies the development, deployment, and management of applications based on the three-tier architecture. By using Docker containers for each tier, developers can achieve consistency, portability, and scalability in their applications, leading to faster development cycles and more efficient deployment processes.


# My Frontend website
![image](https://github.com/DhvaniPatel30/21BCP116_blogpost/assets/126047632/8610267b-4527-4c87-ba79-11a1952df320)

# My Backend 
![image](https://github.com/DhvaniPatel30/21BCP116_blogpost/assets/126047632/db329d64-5df6-4ea9-b2ed-b46c3acd03d9)

# Docker Hub Repository with 3 images
![image](https://github.com/DhvaniPatel30/21BCP116_blogpost/assets/126047632/09ffc7a6-eb64-4dff-aa30-fd828e6e401c)

# Link for Three_Tier_Application:
https://github.com/DhvaniPatel30/21BCP116_Three_Tier_Application


## Thank you for visiting the documentation
