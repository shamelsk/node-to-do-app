# Node To Do App

This is a small Node.js to-do application built with Express and EJS. It lets you add, edit, and delete items from a simple task list, and it uses sanitizer and method-override to keep the form flow clean and safer.

## Features

- Add new to-do items from the web UI.
- Edit and delete existing items.
- Run locally with Node.js.
- Run with Docker or Docker Compose.
- Deploy to Kubernetes using the manifests in k8s/.

## Project Layout

- app.js - main Express application.
- views/ - EJS templates for the todo list and edit page.
- Dockerfile - container image for the app.
- docker-compose.yaml - local Docker Compose setup.
- k8s/ - Kubernetes namespace, deployment, and service manifests.
- DevSecOps/ - Jenkins pipeline documentation and automation notes.

## Prerequisites

- Node.js 16+ and npm.
- Docker and Docker Compose.
- Kubernetes cluster and kubectl if you want to deploy to K8s.

## Run Locally

```bash
npm install
npm start
```

Open the app at http://localhost:8000/todo.

## Run With Docker

Build the image:

```bash
docker build -t node-to-do-app:latest .
```

Run the container:

```bash
docker run -d --name node-to-do-app -p 8000:8000 node-to-do-app:latest
```

Open the app at http://localhost:8000/todo.

## Run With Docker Compose

```bash
docker compose up -d
```

If your environment uses the older command, you can run:

```bash
docker-compose up -d
```

The app will be available on port 8000.

## Deploy To Kubernetes

The Kubernetes manifests are under k8s/:

- k8s/namespace.yml creates the nodejs namespace.
- k8s/deployment.yml creates a 3-replica deployment for the app.
- k8s/service.yml exposes the app as a NodePort service on port 30002.

Apply them in order:

```bash
kubectl apply -f k8s/namespace.yml
kubectl apply -f k8s/deployment.yml
kubectl apply -f k8s/service.yml
```

Then open the app using your cluster node IP and NodePort 30002.

## Tests

Run the project tests with:

```bash
npm test
```

## Notes

- The app currently keeps todo items in memory, so the list resets when the process restarts.
- The Docker and Kubernetes examples use the image naming convention already present in this repository. Update it if you publish your own image.
