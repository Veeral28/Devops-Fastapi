# 🚀 Continuous Delivery of a Dockerized FastAPI Application using GitHub Actions

## 📌 Project Overview
This project demonstrates **Continuous Delivery** by automating the **creation and deployment** of a **Dockerized FastAPI application** using **GitHub Actions**. It ensures that every push to the repository triggers an automated build and pushes the Docker image to Docker Hub.

---

## 📁 Project Structure
```
📦 fastapi-cd
 ┣ 📜 main.py                 # FastAPI Server
 ┣ 📜 requirements.txt        # Dependencies
 ┣ 📜 Dockerfile              # Containerization Setup
 ┣ 📂 .github/workflows/
 ┃ ┗ 📜 DockerBuild.yml      # GitHub Actions Workflow
 ┗ 📜 README.md              # Project Documentation
```

---

## 🛠️ Setup and Run Locally

### 🔹 Prerequisites
- Python 3.8+
- Docker or Podman (Optional)
- GitHub Account
- Docker Hub Account

### 🔹 Installation Steps
1. **Clone the repository**
   ```bash
   git clone https://github.com/<your-github-username>/fastapi-cd.git
   cd fastapi-cd
   ```
2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```
3. **Run the FastAPI server**
   ```bash
   uvicorn main:app --host 0.0.0.0 --port 8000
   ```
4. **Test the API**
   Open your browser and go to:
   ```
   http://127.0.0.1:8000/
   ```
   or test using:
   ```bash
   curl http://127.0.0.1:8000/
   ```

---

## 🐳 Build and Run Docker Image

### 🔹 Build Docker Image
```bash
docker build -t <your-dockerhub-username>/fastapi-app:latest .
```

### 🔹 Run Docker Container
```bash
docker run -p 8000:8000 <your-dockerhub-username>/fastapi-app:latest
```

### 🔹 Test the API (in container)
```bash
curl http://127.0.0.1:8000/
```

---

## ⚙️ GitHub Actions Workflow
### 🔹 How It Works
1. **Trigger:** Runs on every `push` to the repository.
2. **Builds the Docker image** using the `Dockerfile`.
3. **Authenticates with Docker Hub** using a GitHub Secret `DOCKERTOKEN`.
4. **Pushes the built image** to Docker Hub.

### 🔹 Workflow File (`.github/workflows/DockerBuild.yml`)
```yaml
name: Docker Image Build & Push

on: push

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v1
      - name: Build & Push Docker Image
        run: |
          echo ${{ secrets.DOCKERTOKEN }} | docker login -u "<your-dockerhub-username>" --password-stdin
          docker build -t <your-dockerhub-username>/fastapi-app:latest .
          docker push <your-dockerhub-username>/fastapi-app:latest
```

---

## 🔑 Setting Up GitHub Secrets
### 1️⃣ Generate a Docker Hub Access Token
1. Go to **[Docker Hub](https://hub.docker.com/)** → Log in.
2. Navigate to **Account Settings** → **Security** → **Access Tokens**.
3. Click **Generate Token**, copy the token.

### 2️⃣ Add Secret to GitHub
1. Go to **GitHub Repository** → **Settings** → **Secrets** → **Actions**.
2. Click **New repository secret**.
3. Name it **DOCKERTOKEN** and paste the token.

---

## 📌 Submission Requirements
✅ **GitHub Repository URL**: [GitHub Repo](https://github.com/<your-github-username>/fastapi-cd)

✅ **Docker Hub Image URL**: [Docker Hub Image](https://hub.docker.com/r/<your-dockerhub-username>/fastapi-app)

---

## 🔥 Additional Notes
- If using **Podman**, set it up as:
  ```bash
  podman machine init
  podman machine start
  alias docker=podman
  docker --version
  ```
- Ensure **ports are exposed** properly in the `Dockerfile`.
- Monitor **GitHub Actions logs** to debug any errors.

---



💡 **Happy Coding! 🚀**

