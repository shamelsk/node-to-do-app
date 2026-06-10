# DevSecOps Jenkins Pipeline

This folder documents the Jenkins pipeline used to build, scan, and deploy the Node To Do App in this repository. The pipeline is defined in Jenkinsfile and follows the same app and image naming used across the project.

## What The Pipeline Does

- Clones the application source from this repository.
- Runs SonarQube analysis using the configured scanner named Sonar.
- Waits for SonarQube quality gate results.
- Runs OWASP Dependency-Check.
- Builds the Docker image.
- Scans the image with Trivy.
- Pushes the image to Docker Hub.
- Deploys the app with Docker Compose.

## Requirements

- Jenkins installed on a Linux host or VM.
- Docker and Docker Compose installed on the Jenkins machine.
- SonarQube server running and reachable from Jenkins.
- Trivy installed on the Jenkins machine.
- Jenkins plugins for SonarQube, Docker, and OWASP Dependency-Check.
- Docker Hub credentials stored in Jenkins as DockerHubCreds.

## Jenkins Setup

1. Install the required plugins in Jenkins.
2. Configure a SonarQube server entry under Jenkins global tools or system settings.
3. Add a SonarQube scanner installation and name it Sonar.
4. Add a Dependency-Check tool installation and name it OWASP.
5. Add Docker Hub credentials with the ID DockerHubCreds.
6. Create or update the SonarQube webhook so Jenkins can receive the quality gate callback.

## Pipeline Flow

The pipeline in Jenkinsfile currently performs these stages:

```groovy
stage("Code")
stage("SonarQube Analysis")
stage("SonarQube Quality Gates")
stage("OWASP")
stage("Build & Test")
stage("Trivy")
stage("Push to Private Docker Hub Repo")
stage("Deploy")
```

## Notes On The Current Configuration

- The pipeline pulls from https://github.com/shamelsk/node-to-do-app.git on the main branch.
- The Docker image tag used in the Jenkinsfile is shamelsk/node-to-do-app:latest.
- The app container listens on port 8000.
- The deploy step uses docker-compose down && docker-compose up -d.

## If You Want To Run The Same App Manually

Use the root project README for the local, Docker, and Kubernetes steps. This folder is only for the DevSecOps workflow and Jenkins orchestration.
