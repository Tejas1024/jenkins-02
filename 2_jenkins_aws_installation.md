# 2_jenkins_aws_installation.md

# Steps to Install Jenkins in AWS (Ubuntu Instance)

These are exact and corrected steps to set up Jenkins manually on an AWS EC2 Ubuntu instance.

---

## 🧠 Steps:

1️⃣ **Launch EC2 Instance**
- Type: t2.medium
- Minimum 16GB storage
- OS: Ubuntu
- Open port 8080 in Security Group (for Jenkins UI)

2️⃣ **Connect to EC2 via Terminal**
ssh -i <your-key.pem> ubuntu@<public-ip>

text

3️⃣ **Update System & Install Java**
sudo apt update
sudo apt install openjdk-17-jdk -y

text

4️⃣ **Add Jenkins Repository Key & Install Jenkins**
sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key

echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/" | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt update
sudo apt install jenkins -y

 

5️⃣ **Start and Check Jenkins Status**
sudo systemctl start jenkins
sudo systemctl status jenkins

 

6️⃣ **Access Jenkins in Browser**
Go to:  
http://<EC2-Public-IP>:8080

7️⃣ **Get Initial Admin Password**
sudo cat /var/lib/jenkins/secrets/initialAdminPassword

 
Copy the password shown on screen.

8️⃣ **Complete Setup**
- Paste password into Jenkins UI.
- Click “Install suggested plugins.”
- Create admin user (username, password, email).
- Click “Start Jenkins.”
- Jenkins is ready to use! ✅