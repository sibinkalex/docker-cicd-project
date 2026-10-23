# 1. Project overview

## Goal
Automate deployment of a simple website. A push to GitHub triggers Jenkins; Jenkins checks out the code, builds a Docker image, and replaces the running container.

## Components

| Component | Responsibility |
|---|---|
| GitHub | Stores the application and pipeline files |
| GitHub webhook | Sends push events to Jenkins |
| Jenkins | Runs the pipeline |
| Docker image | Packages the site with Nginx |
| Container | Runs Nginx |
| EC2 Ubuntu | Hosts Jenkins and the app container in this lab |
| Browser | Confirms the new page is live |

## Pipeline stages

**Checkout**
```groovy
checkout scm
```
Checks out the configured repository and branch.

**Build**
```bash
docker build -t cicd-webapp:latest .
```
Builds an image using the root `Dockerfile`.

**Deploy**
```bash
docker rm -f cicd-test || true
docker run -d --name cicd-test -p 8081:80 cicd-webapp:latest
```
Removes the old lab container if present, then starts a new one. Host port 8081 forwards to container port 80.

## Lab vs production
Jenkins and the app container share one EC2 instance for simplicity. Production deployments need stronger access controls, HTTPS, secrets management, health checks, rollback, and a more isolated build/deploy design.
