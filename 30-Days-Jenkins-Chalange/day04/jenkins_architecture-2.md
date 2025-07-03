# Jenkins Master-Agent Hands-on Lab Setup Guide (Docker & AWS EC2)

## 🚀 Contents
- Prerequisites
- Jenkins Master setup using Docker
- Jenkins Agent setup using Docker
- Jenkins Master-Agent setup using AWS EC2
- Testing the pipeline across agents
- Cleanup steps

---

## Prerequisites
- Docker installed on your system.
- AWS CLI configured with EC2 access (for EC2 setup).
- Basic understanding of SSH keys.

---

## Jenkins Master Setup Using Docker
```bash
docker run -d \
  --name jenkins-master \
  -p 8080:8080 -p 50000:50000 \
  -v jenkins_home:/var/jenkins_home \
  jenkins/jenkins:lts
```
- Access Jenkins at `http://localhost:8080`.
- Unlock Jenkins using the admin password from:
```bash
docker exec jenkins-master cat /var/jenkins_home/secrets/initialAdminPassword
```
- Install suggested plugins and create your admin user.

---

## Jenkins Agent Setup Using Docker
- Create an agent container:
```bash
docker run -d \
  --name jenkins-agent \
  --init \
  jenkins/agent java -jar /usr/share/jenkins/agent.jar
```
- Alternatively, manually configure nodes in **Manage Jenkins > Nodes > New Node**.
- Use the agent's container IP and port 50000 for inbound connection.

---

## Jenkins Master-Agent Setup Using AWS EC2

### 1️⃣ Launch EC2 Instances
- Launch 1 EC2 for Jenkins Master (Ubuntu 22.04 recommended).
- Launch 1 or more EC2 for Jenkins Agent.
- Open ports 8080 (UI), 50000 (agent connection), and SSH (22).

### 2️⃣ Install Jenkins on Master EC2
```bash
sudo apt update && sudo apt install -y openjdk-17-jdk
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt update && sudo apt install -y jenkins
sudo systemctl enable jenkins && sudo systemctl start jenkins
```
- Access `http://<master-ec2-public-ip>:8080`.
- Retrieve the initial password:
```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

### 3️⃣ Install Java on Agent EC2
```bash
sudo apt update && sudo apt install -y openjdk-17-jdk
```
- Add the agent in Jenkins Master under **Manage Jenkins > Nodes > New Node**.
- Choose **SSH** method, provide the agent's public IP and SSH key credentials.

---

## Testing the Pipeline Across Agents
1. Create a **Freestyle project or Pipeline**.
2. Restrict it to run on the agent using **Labels**.
3. Example Pipeline:
```groovy
pipeline {
  agent { label 'docker-agent' }
  stages {
    stage('Checkout') {
      steps {
        git 'https://github.com/<your-repo>.git'
      }
    }
    stage('Build') {
      steps {
        sh 'echo Building...'
      }
    }
    stage('Test') {
      steps {
        sh 'echo Testing...'
      }
    }
    stage('Deploy') {
      steps {
        sh 'echo Deploying...'
      }
    }
  }
}
```
4. Run the pipeline to verify it executes on the designated agent.

---

## Cleanup Steps
- To stop and remove Docker containers:
```bash
docker stop jenkins-master jenkins-agent
docker rm jenkins-master jenkins-agent
docker volume rm jenkins_home
```
- For EC2, terminate instances from AWS Console when done.

---

✅ You now have a **complete Jenkins Master-Agent hands-on lab guide using Docker & AWS EC2** for your structured DevOps practice folders.

If you would like, I can also prepare a **color diagram (.png) summarizing the architecture** for your quick recall and notes.

