# Experiment 3: Microservices with Docker and Docker Compose

## Objective
To understand microservices architecture and implement a multi-container application using Docker Compose with Flask web service and MySQL database.

## Materials
- Docker Desktop
- Text editor (VS Code/Notepad)
- Terminal/PowerShell
- Web browser for testing

## Prerequisites
- Docker and Docker Compose installed
- Basic understanding of Flask and MySQL
- Project folder structure knowledge

## Procedure

### Step 1: Create Project Structure
```bash
mkdir microservice-app
cd microservice-app
mkdir app db
```

**Project Structure:**
```
microservice-app/
├── app/
├── db/
└── docker-compose.yml
```

### Step 2: Create Flask Application

#### app/app.py
```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def home():
    return "Welcome to Microservice!"

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
```

#### app/requirements.txt
```
flask
```

#### app/Dockerfile
```dockerfile
FROM python:3.9-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
CMD ["python", "app.py"]
```

### Step 3: Create Docker Compose Configuration

#### docker-compose.yml
```yaml
version: '3'
services:
  web:
    build: ./app
    ports:
      - "5000:5000"
    depends_on:
      - db
  
  db:
    image: mysql:5.7
    restart: always
    environment:
      MYSQL_DATABASE: sampledb
      MYSQL_USER: user
      MYSQL_PASSWORD: password
      MYSQL_ROOT_PASSWORD: rootpass
    ports:
      - "3306:3306"
```

### Step 4: Run the Setup
```bash
# Build and start all services
docker-compose up --build

# Run in detached mode (background)
docker-compose up -d --build
```

### Step 5: Test the Application
- Open browser and navigate to: `http://localhost:5000`
- Expected output: "Welcome to Microservice!"

### Step 6: Verify Database Service
```bash
# Check running containers
docker ps

# Access MySQL container (optional)
docker exec -it <db_container_id> mysql -u root -p
# Enter password: rootpass
```

### Step 7: Stop and Clean Up
```bash
# Stop all services
docker-compose down

# Remove volumes (optional)
docker-compose down -v
```

## Service Configuration Details

### Web Service
- **Port**: 5000
- **Dependencies**: Database service
- **Build**: Custom Flask application from ./app directory

### Database Service
- **Image**: MySQL 5.7
- **Port**: 3306
- **Database Name**: sampledb
- **User**: user
- **Password**: password
- **Root Password**: rootpass

## Expected Results
- Both web and database containers running successfully
- Flask application accessible at `http://localhost:5000`
- MySQL database available on port 3306
- Services can communicate with each other via Docker network

## Architecture Benefits
1. **Isolation**: Each service runs in its own container
2. **Scalability**: Services can be scaled independently
3. **Maintainability**: Services can be updated without affecting others
4. **Portability**: Entire application stack is containerized

## Troubleshooting
- **Port conflicts**: Change port mapping in docker-compose.yml
- **Build failures**: Check Dockerfile syntax and file paths
- **Database connection issues**: Verify environment variables and network connectivity
- **Services not starting**: Check docker-compose.yml indentation and syntax

## Conclusion
This experiment demonstrates microservices architecture using Docker Compose. It shows how to orchestrate multiple containers, manage dependencies, and create a networked application environment suitable for modern cloud deployments.
