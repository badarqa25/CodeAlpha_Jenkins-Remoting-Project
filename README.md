# 🚀 Jenkins Remoting Project

This project demonstrates how to set up **Jenkins Remoting** to connect remote Jenkins nodes, distribute builds across different machines, run jobs on multiple architectures, and improve security using node isolation.  

It was implemented on **Ubuntu VM** (with VS Code) and extended using **Docker** to simulate multiple remote agents.

---

## 📌 Project Objectives
- ✅ Set up Jenkins Remoting to connect remote Jenkins nodes  
- ✅ Distribute build loads across different machines securely  
- ✅ Run jobs on various architectures remotely  
- ✅ Improve security using node isolation  
- ✅ Gain hands-on experience with Jenkins’ remote execution capabilities  

---

## 🖥️ Project Architecture

| Jenkins Controller | <-----> | Agent-1 (VM) | <-----> | Agent-2 (Docker) |
| (Ubuntu VM) | | Label: linux | | Label: docker-ubuntu |
| Label: master | | | | |
+--------------------+ +------------------+ +----------------------+

markdown
Copy
Edit

- **Controller** → Central Jenkins server (manages jobs, UI, plugins).  
- **Agent-1** → A permanent agent running directly on the Ubuntu VM.  
- **Agent-2** → A Docker container acting as a remote build node.  

---

## ⚙️ Step-by-Step Setup

### **Step 1: Install Jenkins Controller**
- Installed Java 17  
- Added Jenkins repository and installed Jenkins  
- Started Jenkins on port `8080`  
- Unlocked Jenkins with initial admin password  
- Installed suggested plugins & created admin user  

### **Step 2: Add Remote Agent Node**
- Created a dedicated `jenkins-agent` user  
- Installed Java on agent  
- Downloaded `agent.jar`  
- Connected to Jenkins via:
  ```bash
  java -jar agent.jar -jnlpUrl http://<controller-ip>:8080/computer/agent-1/jenkins-agent.jnlp -secret <secret-key> -workDir "/home/jenkins-agent"
Verified node came online

**Step 3: Distribute Build Loads**

Assigned labels to nodes:

Controller → master

Agent-1 → linux

Agent-2 → docker-ubuntu

Created jobs restricted to specific nodes using label expressions

Verified jobs executed on the correct machine

**Step 4: Security with Node Isolation**

Agents run as non-root users

Enabled Agent-to-Controller Access Control

Applied firewall rules (only 8080 + agent port allowed)

(Optional) Used SSH agents for secure connections

**Step 5: Multi-Architecture Execution**

Added Docker container as Agent-2

Ran jobs on:

Controller (master)

Agent-1 (linux)

Agent-2 (docker-ubuntu)

Verified remote execution via system info (uname -m, lsb_release -d)
