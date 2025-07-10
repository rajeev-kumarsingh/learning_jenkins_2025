# Day-07: Tasks

1. []- Testing Build Artifacts
2. []- Pipeline Graph View
3. []- Defining Environment Variable
4. []- Website project Overview (Clone https://github.com/rajeev-kumarsingh/learn-jenkins-app.git) under
   `~/Documents/DEVOPS/learn-jenkins-app`
5. Troubleshooting Jenkins while using Docker in Jenkinsfile

---

# Troubleshooting Jenkins while using Docker in Jenkinsfile

> IMPORTANT: Read the following text regardless of whether you are experiencing an issue right now or not.

- If you are having difficulties running the pipeline when you want to use a Docker container, open the Docker Desktop app and inspect the containers currently running.
  ![docker desktop](./img/docker-desktop)
- In the screenshot above, you can notice that one container is running (status Running) while the other has the status Exited (255). In this case, Jenkins will not be able to run a stage in a Docker container.
- To fix the issue, run the following commands while the terminal window is in the the `install-jenkins-docker` folder.

1. docker compose down
2. docker compose up -d
   ![docker desktop](./img/docker-desktop-1)
