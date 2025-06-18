# devops_lab_

# Experiment 2: Docker Installation, Containerization & Deployment

## Objective
To install Docker, understand and use containerization commands, create Docker containers with various operating system images, and deploy containerized applications using Docker and Docker Hub.

## Materials
- Ubuntu/Windows with WSL2
- Internet connection
- Text editor (VS Code/Notepad)
- Docker Desktop for Windows

## Prerequisites
- Java JDK 11 (for SonarQube integration)
- Git configured with user credentials

## Procedure

### Step 1: Install Docker
```bash
# Update package list (Ubuntu/WSL)
sudo apt update

# Install Docker engine
sudo apt install docker.io -y

# Start Docker service
sudo systemctl start docker

# Enable Docker to start on boot
sudo systemctl enable docker
```

### Step 2: Verify Docker Installation
```bash
# Check Docker version
docker --version

# Display Docker system information
docker info
```

### Step 3: Pull and Run Docker Images
```bash
# Download Ubuntu OS image
docker pull ubuntu

# Start interactive Ubuntu container
docker run -it ubuntu

# Exit container
exit
```

### Step 4: Manage Docker Containers
```bash
# List running containers
docker ps

# List all containers (including stopped)
docker ps -a

# Stop a running container
docker stop <container_id>

# Remove a stopped container
docker rm <container_id>
```

### Step 5: Manage Docker Images
```bash
# List all downloaded images
docker images

# Remove an image
docker rmi <image_name>
```

### Step 6: Create Flask Application

#### Create app.py
```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def home():
    return "Hello from Docker!"

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
```

#### Create requirements.txt
```
flask
```

#### Create Dockerfile
```dockerfile
FROM python:3.8-slim
WORKDIR /app
COPY . .
RUN pip install -r requirements.txt
CMD ["python", "app.py"]
```

### Step 7: Build and Run Docker Container
```bash
# Build Docker image
docker build -t flask-app .

# Run container in detached mode
docker run -d -p 5000:5000 flask-app

# Access application at http://localhost:5000
```

### Step 8: Push Image to Docker Hub
```bash
# Login to Docker Hub
docker login

# Tag image with username
docker tag flask-app your_dockerhub_username/flask-app

# Push image to Docker Hub
docker push your_dockerhub_username/flask-app

# Logout from Docker Hub
docker logout
```

## Expected Results
- Docker installed and running successfully
- Flask application accessible at `http://localhost:5000`
- Container shows "Hello from Docker!" message
- Image successfully pushed to Docker Hub

## Troubleshooting
- **Port already in use**: Stop existing containers using `docker stop <container_id>`
- **Permission denied**: Use `sudo` for Docker commands or add user to docker group
- **Container not accessible**: Ensure host is set to `"0.0.0.0"` in Flask app

## Conclusion
This experiment demonstrates Docker installation, basic container management, and deployment of a containerized Flask application. Understanding these concepts is crucial for modern DevOps practices and CI/CD implementation.
