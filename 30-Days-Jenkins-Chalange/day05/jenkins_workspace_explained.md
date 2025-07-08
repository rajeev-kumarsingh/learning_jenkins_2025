
# Jenkins Workspace Explained

## What is Jenkins Workspace?

In Jenkins, the **workspace** is a directory on the Jenkins agent (or master) node where Jenkins executes the job builds. Every time a job is run, Jenkins checks out the source code and executes build steps inside this workspace.

Each Jenkins job has its own **dedicated workspace** directory. This directory is used for:
- Storing checked-out code from version control.
- Running build commands (e.g., compilation, testing).
- Storing build artifacts, logs, and temporary files.

---

## Default Workspace Path

By default, Jenkins workspaces are located at:

```
/var/lib/jenkins/workspace/<job-name>/
```

If you're using a Jenkins agent node, the workspace path will be on that agent node.

---

## Example: Understanding Jenkins Workspace

### Jenkins Job: `demo-java-app`

Suppose you have a Jenkins job called `demo-java-app`. When you trigger this job, Jenkins does the following:

1. Creates or reuses the workspace directory:
   ```bash
   /var/lib/jenkins/workspace/demo-java-app/
   ```

2. Checks out the code from GitHub into that directory.
   ```bash
   git clone https://github.com/example/demo-java-app.git
   ```

3. Executes build commands:
   ```bash
   cd /var/lib/jenkins/workspace/demo-java-app/
   mvn clean install
   ```

4. Stores artifacts and test results in the workspace or archives them.

---

## Jenkins Pipeline Example

```groovy
pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/example/demo-java-app.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Workspace Inspection') {
            steps {
                sh 'echo Current Workspace: $WORKSPACE'
                sh 'ls -l $WORKSPACE'
            }
        }
    }
}
```

**Explanation:**
- `agent any`: Runs the pipeline on any available Jenkins agent.
- `WORKSPACE`: Environment variable that points to the workspace directory for this job.
- `ls -l $WORKSPACE`: Lists files in the workspace to inspect its contents.

---

## Cleaning Workspace

You can configure Jenkins to **clean the workspace before/after** a build using the **Workspace Cleanup Plugin**.

```groovy
post {
    always {
        cleanWs()
    }
}
```

This helps in avoiding leftover files from previous builds.

---

## Summary

| Component            | Description                                     |
|----------------------|-------------------------------------------------|
| `$WORKSPACE`         | Environment variable holding workspace path     |
| Job-specific folder  | `/var/lib/jenkins/workspace/<job-name>/`       |
| Contents             | Source code, logs, artifacts, temporary files   |
| Customization        | Can be cleaned using plugins or pipeline steps |

---

## References

- Jenkins Documentation: https://www.jenkins.io/doc/
- Pipeline Syntax: https://www.jenkins.io/doc/book/pipeline/syntax/
