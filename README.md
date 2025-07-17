# Node‑Todo‑CI/CD

A Node.js “To‑Do” app running inside Docker, hosted on an AWS EC2 instance, with full **CI/CD** using **GitLab**.

---

## 🧰 Technology Stack

| Layer           | Tools & Services                   |
|----------------|------------------------------------|
| App             | Node.js, Express, EJS templates    |
| Containerization| Docker, Docker‑Compose             |
| CI/CD           | GitLab CI/CD with a self‑hosted runner |
| Hosting         | AWS EC2 (Ubuntu)                   |

---

## 🚀 Features

- Basic to‑do app with add, edit, delete tasks via web interface
- Packaged in Docker container (`Dockerfile`, `docker-compose.yaml`)
- Fully automated CI/CD:
  1. Builds a Docker image (`docker build`)
  2. Runs unit tests / smoke tests (`echo "testing ..."`)
  3. Pushes image to DockerHub using `$DOCKERHUB_USER` / `$DOCKERHUB_PASS`
  4. Deploys the container on EC2 using `docker-compose up -d`

---

## ⚙️ Deployment Setup on AWS EC2

1. **EC2 instance creation** (Ubuntu):
   - Open ports for SSH, 3000 (Node) and Docker if needed.
2. **Install Docker & Docker‑Compose**:
   ```bash
   sudo apt update
   sudo apt install -y docker.io docker-compose
   sudo usermod -aG docker gitlab-runner
   sudo systemctl restart gitlab-runner
Clone the repo:

git clone https://gitlab.com/mansip140904/node-todo-cicd.git
Run manually (without CI):


docker-compose up -d
App will be accessible at http://<EC2_IP>:3000.

🔁 GitLab CI/CD Pipeline

build – builds the Docker image

test – runs smoke tests

push_to_dockerhub – authenticates and pushes image to DockerHub

deploy – updates the app via docker-compose on EC2

Make sure in GitLab CI/CD Settings → Variables, you’ve defined:

DOCKERHUB_USER

DOCKERHUB_PASS (or better, a token)

⚠️ Troubleshooting Common Issues
docker: command not found → Add GitLab runner user to docker group and restart the service.

Cannot perform an interactive login… → Use echo "$DOCKERHUB_PASS" | docker login … --password-stdin to prevent TTY issues.

✅ Summary
This project demonstrates a clean, Dockerized Node.js application — managed and deployed with automated CI/CD using GitLab to an AWS EC2 host.

Everything from code push to live deployment is handled by the pipeline!
ated testing

Monitor application health

Enable zero-downtime deployments
