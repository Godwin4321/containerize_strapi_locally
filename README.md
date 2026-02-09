
# Strapi Docker Containerization Guide

## Application Without Containerization

Right now your app runs like this:

```
Your Laptop
 ├─ Node.js installed
 ├─ npm installed
 ├─ Dependencies installed
 └─ Strapi running
```

### Problems

- Works only on YOUR machine
- Version differences break apps
- Hard to deploy

---

## Containerization Solves This

Docker packages everything into one unit:

```
Container
 ├─ OS layer
 ├─ Node.js
 ├─ Dependencies
 ├─ Strapi app
 └─ Database files
```

So anyone can run your app using just:

```bash
docker run ...
```

No setup needed.  
That’s why companies containerize applications.

---

## What Is a Dockerfile?

A Dockerfile is like a **recipe** to build your application container.

It tells Docker:

- Which base OS to use
- Install Node
- Copy project files
- Install dependencies
- Start the app

---

## Task Goal

1. Create Dockerfile  
2. Build image  
3. Run container  
4. Access Strapi admin panel  

---

## Create Dockerfile

Inside `strapi-app` folder:

```bash
nano Dockerfile
```

Paste:

```dockerfile
# Use official Node image
FROM node:20

# Set working directory
WORKDIR /app

# Copy package files first
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy remaining project files
COPY . .

# Build admin panel
RUN npm run build

# Expose Strapi port
EXPOSE 1337

# Start Strapi
CMD ["npm", "run", "develop"]
```

---

## Dockerfile Explanation

| Instruction | Purpose |
|------------|---------|
| FROM node:20 | Base Node image |
| WORKDIR /app | App directory |
| COPY package*.json | Copy dependency list |
| RUN npm install | Install dependencies |
| COPY . . | Copy project |
| RUN npm run build | Build admin panel |
| EXPOSE 1337 | Open Strapi port |
| CMD npm run develop | Start server |

---

## Install Docker

```bash
sudo apt update
sudo apt install -y docker.io
```

Start & enable:

```bash
sudo systemctl start docker
sudo systemctl enable docker
```

Verify:

```bash
docker --version
```

---

## Fix Docker Permissions

```bash
sudo usermod -aG docker $USER
newgrp docker
```

Test:

```bash
docker run hello-world
```

---

## Build Docker Image

```bash
docker build -t strapi-app .
```

---

## Important DevOps Principle

Never copy `node_modules` into Docker images.

Use `.dockerignore` to exclude:

```
node_modules
.git
dist
database
.env
```

---

## Rebuild Clean Image

```bash
docker build --no-cache -t strapi-app .
```

---

## Environment Variable Configuration

If Strapi fails due to missing secrets, run:

```bash
docker run -p 1337:1337 -e ADMIN_JWT_SECRET=myadminsecret -e APP_KEYS=myappkey1,myappkey2 -e API_TOKEN_SALT=myapitokensalt strapi-app
```

---

## Push Image to Docker Hub

Tag image:

```bash
docker tag strapi-app YOUR_USERNAME/strapi-app:latest
```

Push:

```bash
docker push YOUR_USERNAME/strapi-app:latest
```

---

## Image Registries

Docker images can be stored in:

- Docker Hub
- AWS ECR
- Google Artifact Registry
- Azure Container Registry
- GitHub Container Registry

---

## Summary

You successfully:

- Containerized Strapi
- Built Docker image
- Ran container locally
- Managed environment variables
- Pushed image to registry

This demonstrates real DevOps containerization workflow.