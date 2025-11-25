# 3_github_jenkins_webhook.md

# Webhook (GitHub → Jenkins Auto Build)

---

## 💡 What is a Webhook?

A Webhook is a way for GitHub to automatically send a signal to Jenkins whenever code changes occur — without Jenkins polling periodically.

Instead of Jenkins checking GitHub every 5 mins (Poll SCM),  
→ GitHub instantly notifies Jenkins when a commit/push happens.

---

## ⚙️ Flow Diagram (conceptual)
GitHub Repo ---> Webhook URL ---> Jenkins Job
(push) (POST) (build)

 

---

## 🧩 Working Concept:

- Developer pushes code to GitHub.
- GitHub sends an HTTP POST request to Jenkins via a Webhook URL.
- Jenkins receives the request and triggers the build immediately.

---

## 🧠 Steps to Set Up Webhook in Jenkins

**Step 1: Enable Jenkins Job for Webhook**  
In Jenkins, open your job → Configure → Build Triggers →  
Check ✅ "GitHub hook trigger for GITScm polling" → Save.

**Step 2: Get Jenkins Webhook URL**  
Format:  
`http://<Jenkins-IP>:8080/github-webhook/`

Example:  
`http://13.126.45.89:8080/github-webhook/`

**Step 3: Configure in GitHub**  
- Open GitHub repo → Settings → Webhooks  
- Click Add Webhook  
- Enter Payload URL: `http://<Jenkins-IP>:8080/github-webhook/`  
- Content type → application/json  
- Choose “Just the push event”  
- Add Webhook  

**Step 4: Test It**  
- Make a code change → Commit & Push  
- Jenkins should immediately trigger a build.

---

## 🧩 Why Webhooks Are Better Than Poll SCM?

| Feature           | Poll SCM                       | Webhook                        |
|------------------|------------------------------|------------------------------|
| Trigger timing    | Periodic check (e.g. every 5 mins) | Immediate (on push)           |
| Server load       | High (frequent checks)         | Low                          |
| Real-time response| No                            | Yes                          |
| Internet dependency | Jenkins initiates             | GitHub initiates             |

---

## ⚙️ Note:
If webhook doesn’t work:  
- Jenkins URL must be publicly accessible (not localhost).  
- Port 8080 is open in AWS security group.  
- Jenkins plugin “GitHub Integration Plugin” installed.

---

## ✅ Summary:

| Concept               | Description                              |
|-----------------------|----------------------------------------|
| Build after other projects | Chain multiple Jenkins jobs           |
| AWS Jenkins Setup     | Install Jenkins on Ubuntu EC2           |
| Webhook               | GitHub instantly triggers Jenkins build|
| Poll SCM vs Webhook   | Poll SCM checks periodically; webhook triggers immediately 
