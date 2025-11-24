# 6_mock_interview_task.md

# Mock Interview Task: Jenkins CI/CD Pipeline

---

## Task:
Write a Jenkinsfile that:
- Pulls code from GitHub.
- Runs a Maven build.
- Publishes build artifacts.
- Deploys WAR file to Tomcat server.

---

## Complete Jenkinsfile Example:

pipeline {
agent any
stages {
stage('Git Checkout') {
steps {
git branch: 'main', url: 'https://github.com/Samplegitid/MyApp.git'
}
}
stage('Build with Maven') {
steps {
sh 'mvn clean package'
}
}
stage('Publish Artifacts') {
steps {
archiveArtifacts artifacts: '/target/*.war', fingerprint: true
}
}
stage('Deploy to Tomcat') {
steps {
sshPublisher(publishers: [
sshPublisherDesc(
configName: 'tomcat-server',
transfers: [
sshTransfer(
sourceFiles: '/target/*.war',
removePrefix: 'target',
remoteDirectory: '/opt/tomcat/webapps'
)
],
usePromotionTimestamp: false
)
])
}
}
}
}

 

---

## Step-by-step Breakdown:

- Pulls code from GitHub repo.
- Builds with Maven → `.war` file.
- Publishes artifact to Jenkins.
- Deploys WAR to Tomcat via SSH plugin.

---

## Additional Setup for Deployment:

- Install "Publish Over SSH" plugin.
- Configure SSH server under Manage Jenkins → Configure System → Publish over SSH.
- Add Tomcat server credentials (IP, username, SSH key/password).

---

# Summary Table

| Concept                | Purpose                             |
|------------------------|-----------------------------------|
| Pipeline               | Defines CI/CD process using stages |
| Agent                  | Node that runs the job             |
| Stage                  | Logical build step                 |
| Role-Based Authorization| Restricts Jenkins access by role |
| Mock Interview Task    | Practice: automated build & deploy |