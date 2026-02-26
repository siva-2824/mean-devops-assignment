#  MEAN Stack Application – Dockerized & CI/CD Deployed on AWS

---

##   Project Overview

This project demonstrates a complete DevOps workflow for deploying a full-stack MEAN (MongoDB, Express, Angular, Node.js) application.

The project includes:

- Docker containerization
- Docker Compose orchestration
- Cloud deployment using AWS EC2
- Nginx reverse proxy setup
- CI/CD automation using GitHub Actions

The goal was to implement automated build and deployment with minimal manual intervention.

---

##   Architecture Overview


Developer → GitHub → GitHub Actions (CI/CD)   
↓   
Docker Hub   
↓   
AWS EC2 (Ubuntu)   
↓   
Docker Compose  
┌──────┬─────┬────────┐   
│ Mongo │      Backend │      Frontend │   
└──────┴─────┴────────┘   
↓   
Nginx (Port 80)   


---

##  Repository Structure


backend/   
Dockerfile

frontend/   
Dockerfile

docker-compose.yml

.github/workflows/
deploy.yml

README.md


---

##  Docker Setup

### Backend

- Node.js based container
- API server running on port 8080
- Connects to MongoDB container

### Frontend

- Angular application
- Multi-stage Docker build
- Served via Nginx container

### MongoDB

- Official MongoDB Docker image
- Persistent storage enabled

---

##  Local Setup Instructions

### Clone repository


git clone https://github.com/siva-2824/mean-devops-assignment



### Run application


docker-compose up -d


### Access application


http://localhost:3000


---

##  Cloud Deployment (AWS EC2)

### Step 1 – Create EC2 Instance

- Ubuntu 22.04
- Instance type: t3.micro (Free tier)
- Open ports:
  - 22 (SSH)
  - 80 (HTTP)
  - 3000
  - 8080

### Step 2 – Install Docker


sudo apt update
sudo apt install docker.io docker-compose -y


### Step 3 – Deploy Application


docker-compose up -d


Application available at:


http://<EC2_PUBLIC_IP>      
MY EC2 http://16.112.12.252

---

##  Nginx Reverse Proxy Configuration

Nginx configured to expose application via port 80.


server {
listen 80;

location / {
    proxy_pass http://localhost:3000;
}

location /api {
    proxy_pass http://localhost:8080;
}

}


---

##  CI/CD Pipeline (GitHub Actions)

Workflow file:


.github/workflows/deploy.yml


Pipeline process:

1. Trigger on push to main branch
2. Build backend Docker image
3. Build frontend Docker image
4. Push images to Docker Hub
5. SSH into AWS EC2
6. Pull latest images
7. Restart containers

---

##  Docker Hub Repositories

- bloodshot2824/backend
- bloodshot2824/frontend

---

##  Screenshots

### CI/CD Execution
<img width="1881" height="790" alt="image" src="https://github.com/user-attachments/assets/2f0d8707-6462-4ecf-a71e-84823f8894cf" />



### Docker Image Build & Push
<img width="1898" height="662" alt="image" src="https://github.com/user-attachments/assets/152237a2-7b67-400e-8adf-3560ef484574" />



### Application Deployment
<img width="1905" height="904" alt="image" src="https://github.com/user-attachments/assets/75f1481c-6ec1-4a6c-9b94-7e4d374a0361" />



### Nginx Setup & Infrastructure
<img width="1781" height="616" alt="image" src="https://github.com/user-attachments/assets/2e81013a-b392-4702-bf29-d7398aa28220" />



---

##  DevOps Concepts Demonstrated

- Docker containerization
- Multi-container orchestration
- Reverse proxy configuration
- Automated CI/CD pipeline
- Cloud infrastructure deployment
- Secure SSH automation

---

##  Author

Siva Bharathi S
