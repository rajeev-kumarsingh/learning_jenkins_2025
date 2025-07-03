# Jenkins Architecture Explained with Example

## 1️⃣ What is Jenkins?

Jenkins is an open-source automation server used for **Continuous Integration (CI) and Continuous Delivery (CD)**, allowing you to automate building, testing, and deploying applications.

## 2️⃣ Core Jenkins Architecture

Jenkins architecture typically follows a **Master-Agent** design:

### **A. Jenkins Master (Controller)**

- **Role:**
  - Manages the orchestration of jobs.
  - Handles web UI, configurations, job scheduling.
  - Dispatches build jobs to agents.
  - Monitors agent statuses.
- **Components:**
  - Web Server
  - Scheduler
  - Build Queue
  - Distributed Builds Manager

### **B. Jenkins Agent (Slave/Worker)**

- **Role:**
  - Executes build jobs dispatched by the master.
  - Can run on different operating systems (Linux, Windows, macOS).
  - Helps scale Jenkins by offloading heavy workloads from the master.
- **Connection:**
  - Agents communicate with the master via SSH or JNLP.
  - Can be static or dynamically provisioned using plugins like Kubernetes, AWS EC2, or Docker.

## 3️⃣ Workflow in Jenkins

1. **Developer commits code** to the Source Code Management (SCM) like GitHub/GitLab.
2. **Jenkins Master detects changes** using Webhooks or Polling.
3. **Job is triggered**, Jenkins master puts the job into the **build queue**.
4. Jenkins master assigns the job to an available **agent** based on labels or availability.
5. The agent **executes the build/test scripts** defined in the pipeline or Freestyle project.
6. Results are sent back to the master.
7. Jenkins Master updates the **build status** and notifies developers via Email/Slack.
8. Optional: Successful builds can be deployed to **staging/production environments** automatically.

## 4️⃣ Example: Jenkins CI Pipeline for a Java Project

- **Project:** Java Spring Boot application.
- **Source Code:** GitHub.
- **Pipeline:**
  - Checkout Code
  - Compile using Maven
  - Run Unit Tests
  - Package as JAR
  - Deploy to a Staging Server (using SSH or Ansible)

### **Flow:**

- Developer commits changes.
- GitHub webhook notifies Jenkins.
- Jenkins triggers the pipeline.
- Master assigns the job to a Linux agent.
- Agent runs `mvn clean package`.
- Unit tests run, and if they pass, the JAR is created.
- Agent copies the JAR to the staging server.
- Developers are notified on Slack about the build status.

## 5️⃣ Jenkins Distributed Build Advantages

- Scalability: Distribute workloads across many agents.
- Efficiency: Run multiple builds in parallel.
- Flexibility: Use different environments for different jobs (Node.js on one agent, Java on another).
- Stability: The master is kept lightweight by offloading heavy builds to agents.

## 6️⃣ Security in Jenkins Architecture

- Use secured communication between master and agents.
- Configure user roles and permissions.
- Secure credentials using Jenkins Credentials Manager.

## 7️⃣ Diagram (Visual Memory)

```
+----------------+           +---------------------+
|   Jenkins      |  SSH/JNLP |    Agent 1          |
|   Master       +---------->+  (Linux)            |
|                |           +---------------------+
|  - Scheduler   |
|  - UI          |           +---------------------+
|  - Queue       +---------->+    Agent 2          |
|                |  SSH/JNLP |   (Windows)         |
+----------------+           +---------------------+
```

## ✅ Summary

- Jenkins uses **Master-Agent architecture** for scalable, distributed CI/CD pipelines.
- The master handles orchestration while agents execute the builds.
- Enables automated builds, tests, and deployments across different environments.
- Supports plugins for cloud, container, and advanced pipeline orchestration.

---

If you need a **hands-on lab setup guide using Docker or AWS EC2 for Jenkins Master-Agent**, let me know for your next practice session.

