# 4_master_slave_architecture.md

# Jenkins Master–Slave Architecture

---

## What is Jenkins Master–Slave Architecture?

A distributed build system in Jenkins that spreads build tasks across multiple machines for faster execution.

---

## ⚙️ Roles Explained:

### 1. Master Node
- Main Jenkins server.
- Manages job scheduling.
- Dispatches builds to slaves.
- Monitors slave nodes.
- Displays build results.

### 2. Slave Node (Agent)
- Machines connected to master.
- Execute the builds, tests, and deployments.
- Can be configured for specific job types.

---

## 💡 Purpose
- Load balancing: Distribute workload.
- Parallel execution: Run multiple builds simultaneously.
- Platform diversity: Run jobs on different OS types.

---

## 🧩 Workflow

- Developer commits code → pushes to repo.
- Master detects changes (poll SCM/webhook).
- Master assigns job to suitable slave.
- Slave runs builds/tests/deployments.
- Results reported to master UI.

---

## 🔧 Setup Steps

### Master Setup
- Launch EC2 instance for master.
- Install Jenkins and dependencies (Java).
- Start Jenkins and configure admin access.

### Slave Setup
- Launch EC2 instance as slave.
- Install Java (required for Jenkins agents).
- From Master Jenkins UI → Manage Jenkins → Manage Nodes → New Node.
- Setup slave details and labels.
- Launch slave with provided JNLP command:

java -jar agent.jar -jnlpUrl http://<master-ip>:8080/computer/slave1/slave-agent.jnlp -secret <secret-key> -workDir "/home/ubuntu"

 

---

## 🧠 Summary Table

| Component | Function                                    |
|-----------|---------------------------------------------|
| Master    | Controls Jenkins environment, schedules jobs |
| Slave     | Executes jobs assigned by master             |
| Labels    | Define slave capabilities                     |
| JNLP      | Protocol for secure agent connection         |

---

## ✅ Real-Life Use Case
Multiple developers push code → master distributes tasks to different slaves → builds/tests/deployments run parallel → faster results.