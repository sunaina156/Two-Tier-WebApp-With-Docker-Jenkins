# Two-Tier Web Application Deployment using Docker, Jenkins & AWS EC2

## Project Overview
This project demonstrates a **two-tier web application architecture** using DevOps practices.

- **Frontend/Backend:** Flask (Python)
- **Database:** MySQL
- **Containerization:** Docker
- **Orchestration:** Docker Compose
- **CI/CD Tool:** Jenkins
- **Cloud Platform:** AWS EC2
- **Image Registry:** Docker Hub

The application is built, pushed, and deployed automatically using a Jenkins CI/CD pipeline.

---

- Flask handles HTTP requests  
- MySQL stores application data  
- Docker Compose manages containers  
- Jenkins automates build and deployment 

---
# Project Structure
Two-Tier-WebApp-With-Docker-Jenkins/
│
├── app.py                 # Flask application
├── requirements.txt      # Python dependencies
├── Dockerfile            # Docker image for Flask app
├── docker-compose.yml    # Multi-container setup
├── Jenkinsfile           # CI/CD pipeline script
│
├── templates/            # HTML templates
│   └── index.html
│
├── mysql-data/           # MySQL persistent data (volume)
├── .dockerignore         # Ignore unnecessary files in Docker build
│
└── README.md             # Documentation

---
## Key DevOps Files

### Dockerfile
Defines the application environment and builds the Flask app image.

### docker-compose.yml
Used to run multi-container application:
- Flask app container
- MySQL database container

### Jenkinsfile
Defines the CI/CD pipeline stages:
- Build Docker image
- Push image to Docker Hub
- Deploy containers using Docker Compose
---

##  AWS EC2 Setup
The project is deployed on an AWS EC2 instance to simulate a real-world production environment

## Steps Performed
1. Launched EC2 instance (Ubuntu) 
   (Instance type Preferred: t3.medium)
   
   Ports opened:
   22 -> SSH
   8080 -> Jenkins
   5000 -> Flask

2. Connected using SSH:
   ssh -i key.pem ubuntu@<EC2-PUBLIC-IP>

3. Installed 
- Docker
  (https://docs.docker.com/engine/install/ubuntu/)
- Docker Compose
  (https://docs.docker.com/compose/)
- Jenkins
  (https://www.jenkins.io/doc/book/installing/linux/)

 

4. Start Services & Configure Permissions

# Start and Enable Services
....................
> sudo systemctl start docker
> sudo systemctl enable docker

> sudo systemctl start jenkins
> sudo systemctl enable jenkins

  
# Add User to Docker Group
..................................
This allows running Docker commands without sudo:

> sudo usermod -aG docker ubuntu
> newgrp docker

# Allow Jenkins to Access Docker
............................................
By default, Jenkins cannot run Docker commands. Grant permissions:
> sudo usermod -aG docker jenkins

Restart Jenkins to apply changes:
> sudo systemctl restart jenkins


---

# Access URLs

- Jenkins:
http://<EC2-PUBLIC-IP>:8080

- Application:
http://<EC2-PUBLIC-IP>:5000

# Jenkins Setup
Unlock Jenkins
> sudo cat /var/lib/jenkins/secrets/initialAdminPassword

Then, install all suggested Plugins

# Add Docker Hub Credentials on Jenkins
Go to: Manage Jenkins → Manage Credentials
Add Credentials:
Kind: Username with Password
Username: Docker Hub username
Password: Docker Hub password
ID: dockerHubCreds

# Create Pipeline Job
Click New Item
Enter name: pipeline-deployment
Select Pipeline
Click OK

# Configure Pipeline

Choose: Pipeline script from SCM
SCM: Git
Repository URL: https://github.com/sunaina156/Two-Tier-WebApp-With-Docker-Jenkins.git
Branch: main
Script Path: Jenkinsfile


Access Application:
http://<EC2-PUBLIC-IP>:5000
(It's running)

