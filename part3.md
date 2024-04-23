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



## Thank you for visiting the documentation
