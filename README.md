
# 🤖 Docker Image Automation Using Jenkins

This project demonstrates the end-to-end automation of **Docker image creation, testing, and pushing to Docker Hub** using **Jenkins**. It's a classic CI/CD pipeline project for container-based DevOps workflows.

---

## 🚀 Objective

Automate the Docker image lifecycle using Jenkins:
- ✅ Build a Docker image from a source code repo
- ✅ Tag it appropriately
- ✅ Push it to Docker Hub
- ✅ Trigger pipeline automatically on GitHub commits

---

## 🛠️ Tools & Technologies

| Tool        | Purpose                          |
|-------------|----------------------------------|
| 🐳 Docker   | Containerize the application     |
| 🧪 Jenkins  | Automate CI/CD pipeline          |
| 💻 GitHub   | Source code repository           |
| 📦 Docker Hub | Docker image registry         |

---

## 📁 Project Structure

```

.
├── Dockerfile
├── Jenkinsfile
├── app/
│   └── index.html / main.py / ...
└── README.md

````

---

## 🔧 Prerequisites

Before getting started, make sure you have the following installed and configured:

- Jenkins (with Docker and GitHub integration)
- Docker Engine
- GitHub account
- Docker Hub account
- Jenkins plugins:
  - Docker Pipeline
  - GitHub
  - GitHub Integration Plugin
  - Pipeline

---

## ⚙️ Jenkins Pipeline Breakdown

### 🔸 1. Clone GitHub Repository

```groovy
git 'https://github.com/abhi-gadge1773/Project-Docker-image-automation-using-Jenkins.git'
````

### 🔸 2. Build Docker Image

```groovy
sh 'docker build -t abhi-gadge1773/myapp:${BUILD_NUMBER} .'
```

### 🔸 3. Push to Docker Hub

```groovy
withDockerRegistry(credentialsId: 'dockerhub-creds', url: '') {
    sh 'docker push abhi-gadge1773/myapp:${BUILD_NUMBER}'
}
```

### 🔸 4. Tag Latest

```groovy
sh 'docker tag abhi-gadge1773/myapp:${BUILD_NUMBER} abhi-gadge1773/myapp:latest'
sh 'docker push abhi-gadge1773/myapp:latest'
```

---

## 🧪 How to Run the Pipeline

1. Clone this repo on your Jenkins server or link via GitHub.
2. Add Docker Hub credentials in Jenkins:

   * Go to **Jenkins → Manage Credentials**
   * Add username/password under ID: `dockerhub-creds`
3. Configure a new **Pipeline Job** in Jenkins.
4. Point it to this repo and use the `Jenkinsfile`.
5. Click **Build Now**.

---

## 📦 Dockerfile Example

```dockerfile
FROM python:3.9-slim

WORKDIR /app

COPY app/ .

CMD ["python3", "app.py"]
```

---

## 📸 Sample Output

```text
Step 1/4 : FROM python:3.9-slim
 ---> 1c6b8935a0c5
Step 2/4 : WORKDIR /app
 ---> Running in 1720e841f...
Step 3/4 : COPY app/ .
 ---> Using cache
Step 4/4 : CMD ["python3", "app.py"]
 ---> Running in 4bd3c40d...
Successfully built <IMAGE_ID>
Successfully pushed to Docker Hub
```

---

## ✅ Output

Docker image will be automatically published to Docker Hub under:
🔗 `https://hub.docker.com/repository/docker/abhi-gadge1773/myapp`

---

## 📌 GitHub Repository

👉 [Project Repository Link](https://github.com/abhi-gadge1773/Project-Docker-image-automation-using-Jenkins.git)

---

## 🙌 Author

**Abhijeet Gadge**
📧 [abhijeetgadge100@gmail.com](mailto:abhijeetgadge100@gmail.com)
🔗 [LinkedIn](https://www.linkedin.com/in/abhijeetgadge/)
🔗 [GitHub](https://github.com/abhi-gadge1773)

---

## ⭐ Support

If this project helped you, please ⭐ star the repo and share it!

---
