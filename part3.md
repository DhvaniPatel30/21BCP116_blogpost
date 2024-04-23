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
![Image](/images/image.png)
## Step 2: Building and Running React Frontend Container
 ``` dockerfile
# Build the Docker image for React frontend
docker build -t 21bcp116-frontend .

# Run the React frontend container
docker run -d --name 21bcp116-frontend -p 80:80 --network my-network 21bcp116-frontend
```

![Image](/images/Screenshot 2024-04-23 115003.png)


![Image](/images/Screenshot 2024-04-23 115136.png)


## Thank you for visiting the documentation