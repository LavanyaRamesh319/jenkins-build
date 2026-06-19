# jenkins-build

# Jenkins Auto-Build with GitHub Integration

This project demonstrates a simple CI/CD pipeline using **Jenkins** and **GitHub**.  
Whenever a commit is pushed to the repository, Jenkins automatically triggers a build, executes a script, and sends the build output via email.

---

## 📂 Project Structure
jenkins-build/
├── hello.sh        # Simple bash script
└── Jenkinsfile     # Jenkins pipeline definition

## 🚀 Steps to Reproduce

### 1. Create Script
```bash
#!/bin/bash
echo "Hello Jenkins Lab! Auto-build triggered at $(date)"

Commit and push to GitHub:
git init
git branch -M main
git add hello.sh
git commit -m "Initial commit with hello.sh"
git remote add origin https://github.com/LavanyaRamesh319/jenkins-build.git
git push -u origin main

### 2. Add Jenkinsfile
pipeline {
    agent any

    stages {
        stage('Run Script') {
            steps {
                sh './hello.sh'
            }
        }
    }

    post {
        success {
            emailext (
                to: 'lavanyaramesh319@gmail.com',
                subject: "Build SUCCESS",
                body: "Build succeeded!"
            )
        }
        failure {
            emailext (
                to: 'lavanyaramesh319@gmail.com',
                subject: "Build FAILED",
                body: "Build failed!"
            )
        }
    }
}

Commit & push:
git add Jenkinsfile
git commit -m "Added Jenkinsfile with email notification"
git push origin main

###3. Configure Jenkins
New Item → Pipeline → Github-Autobuild

Pipeline definition: Pipeline script from SCM

SCM: Git

Repo URL: https://github.com/LavanyaRamesh319/jenkins-build.git

Branch: */main

Script Path: Jenkinsfile

Build Trigger: GitHub hook trigger for GITScm polling

###4. Configure GitHub Webhook
Repo → Settings → Webhooks → Add webhook

Payload URL:
http://<Public-IP>:8080/github-webhook/
Content type: application/json

Trigger: “Just the push event”

###5. Configure Email
Jenkins → Manage Jenkins → Configure System → Extended E-mail Notification

SMTP: smtp.gmail.com

Port: 465 (SSL) or 587 (TLS)

Credentials: Gmail + App Password

Every commit → Jenkins auto-build → Email notification.
