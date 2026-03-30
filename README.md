🚀 Full Stack Spring Boot + MySQL + Docker + Jenkins CI/CD

This project demonstrates a production-ready CI/CD pipeline using:

☕ Spring Boot (Backend)
🐬 MySQL (Database)
🐳 Docker & Docker Compose
🔄 Jenkins Pipeline
☁️ AWS EC2 Deployment
📌 Project Architecture
Developer → GitHub → Jenkins → Docker Build → Docker Hub → AWS EC2 → Run Container
📂 Project Structure
.
├── Dockerfile
├── docker-compose.yml
├── Jenkinsfile
├── pom.xml
└── src/
⚙️ Prerequisites

Make sure you have:

AWS Account (Free Tier)
EC2 Instance (Amazon Linux / Ubuntu)
Docker Installed
Jenkins Installed
Git Installed
Docker Hub Account
☁️ Step 1: Launch AWS EC2
Go to AWS Console
Launch EC2 Instance:
OS: Amazon Linux 2023 / Ubuntu
Instance Type: t2.micro (Free tier)
Allow ports in Security Group:
22 (SSH)
8080 (App)
8081 (App external)
8080 (Jenkins)
3306 (MySQL if needed)
🔐 Step 2: Connect to EC2
ssh -i your-key.pem ec2-user@your-public-ip
🐳 Step 3: Install Docker
Amazon Linux:
sudo yum update -y
sudo yum install docker -y
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker ec2-user
Ubuntu:
sudo apt update
sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker

👉 Re-login after adding docker group

🐙 Step 4: Install Git
sudo yum install git -y     # Amazon Linux
sudo apt install git -y     # Ubuntu
🔄 Step 5: Install Jenkins
sudo yum install java-17-amazon-corretto -y

sudo wget -O /etc/yum.repos.d/jenkins.repo \
https://pkg.jenkins.io/redhat-stable/jenkins.repo

sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key

sudo yum install jenkins -y

sudo systemctl start jenkins
sudo systemctl enable jenkins

Access Jenkins:

http://<EC2-PUBLIC-IP>:8080

Get admin password:

sudo cat /var/lib/jenkins/secrets/initialAdminPassword
⚙️ Step 6: Configure Jenkins
Install Plugins:
Docker Pipeline
Git
Maven Integration
Configure Tools:
Maven → Name: MAVEN
🔑 Step 7: Add Docker Hub Credentials

Go to:

Manage Jenkins → Credentials
Add:
ID: docker
Username: DockerHub username
Password: DockerHub password
📥 Step 8: Create Jenkins Pipeline
New Item → Pipeline
Add your Jenkinsfile
Save & Build
🐳 Step 9: Docker Setup (Manual - Optional)
Run MySQL Container
docker run -d \
--name mysql-container \
-e MYSQL_ROOT_PASSWORD=root \
-e MYSQL_DATABASE=devops_db \
-p 3307:3306 \
mysql:8
🐳 Step 10: Docker Compose (Recommended)
docker-compose up -d
🔄 CI/CD Pipeline Stages
✅ Clone Code from GitHub
🔨 Build JAR using Maven
🐳 Build Docker Image
🔐 Login to Docker Hub
📤 Push Image
🚀 Deploy Container
▶️ Access Application
http://<EC2-PUBLIC-IP>:8081
🧪 Useful Commands
Stop all containers
docker stop $(docker ps -q)
Remove all containers
docker rm -f $(docker ps -aq)
Remove images
docker rmi -f $(docker images -q)
Remove volumes
docker volume prune -f
⚠️ Common Issues & Fixes
❌ Docker Permission Denied
sudo usermod -aG docker ec2-user
❌ Port Already in Use
sudo lsof -i :8081
❌ MySQL Connection Issue
Ensure container name matches:
mysql-container
Check network:
docker network ls
📌 Environment Variables Used
SPRING_DATASOURCE_URL=jdbc:mysql://mysql-container:3306/devops_db
SPRING_DATASOURCE_USERNAME=root
SPRING_DATASOURCE_PASSWORD=root
🎯 Key Features
✔️ Fully Automated CI/CD Pipeline
✔️ Dockerized Spring Boot Application
✔️ MySQL Container Integration
✔️ AWS Deployment Ready
✔️ Production-Level Setup
👨‍💻 Author

Sanket Mahajan
