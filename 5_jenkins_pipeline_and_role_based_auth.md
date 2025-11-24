# 5_jenkins_pipeline_and_role_based_auth.md

# Jenkins Pipeline Overview

A Jenkins Pipeline is a set of automated steps defined in a `Jenkinsfile` using Groovy syntax.

---

## Pipeline Basic Structure

pipeline {
agent any
stages {
stage('StageName') {
steps {
// Commands/scripts here
}
}
}
}

text

---

## Key Concepts:

- **Multibranch Pipeline:** Automatically detects and builds multiple Git branches.
- **Stages:** Logical parts of the CI/CD process (Build, Test, Deploy).
- **Agent:** The node (master/slave) where pipeline executes.
- **Triggers:** Define when to run (pollSCM, Webhook).

---

## Example Jenkinsfile:

pipeline {
agent any
stages {
stage('Git Checkout') {
steps {
git branch: 'main', url: 'https://github.com/Samplegitid/JDP/piping-framework-petclinic.git'
}
}
stage('Build with Maven') {
steps {
sh 'mvn clean package'
}
}
stage('Copy Files to Artifacts') {
steps {
archiveArtifacts artifacts: '**/target/*.war', fingerprint: true
}
}
}
}

text

---

# Role-Based Authorization in Jenkins

Control user access and permissions based on roles.

---

## Steps to Enable:

1. Install Plugin: "Role-based Authorization Strategy" via Manage Jenkins → Manage Plugins.
2. Enable Strategy: Manage Jenkins → Configure Global Security → Authorization → Role-Based Strategy.
3. Create Roles: Manage Jenkins → Manage and Assign Roles → Manage Roles.
   - Global roles (e.g., admin, developer, viewer).
   - Project roles (restrict to specific jobs).
4. Assign Roles: Manage Jenkins → Manage and Assign Roles → Assign Roles.

---

## Example Roles & Permissions

| User    | Role          | Permissions                      |
|---------|---------------|---------------------------------|
| admin   | Global Role   | Full access                    |
| dev_team| Project Role  | Build and view own jobs        |
| tester  | Project Role  | View results only              |