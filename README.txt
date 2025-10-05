# 🧩 Flask AWS Monitor

**Flask AWS Monitor** is a lightweight DevOps infrastructure project designed to demonstrate integration between **AWS**, **Flask**, **Docker**, and **Kubernetes** using **Helm**.  
It provides real-time insights into AWS EC2 instances running under a specific account and can be deployed as a containerized microservice in a Kubernetes cluster.

---

## 🚀 Project Overview

This project was built to showcase cloud automation and infrastructure management skills, including:

- Building and containerizing a Python Flask application.
- Using **Boto3** to fetch and display AWS instance metadata.
- Automating deployment to **Kubernetes** via **Helm charts**.
- Managing scalable infrastructure with Docker images and Kubernetes manifests.

The system can automatically bring up virtual machines in AWS using a custom Docker image and display instance information through a simple Flask interface.

---

## 🏗️ Architecture

**Components:**
1. **Flask App (Python)** — Provides a REST API / web endpoint that queries AWS EC2 instances.
2. **AWS (EC2)** — Cloud infrastructure where instances are managed and monitored.
3. **Boto3** — Python SDK used for interacting with AWS services.
4. **Docker** — The application runs as a Docker container for portability.
5. **Kubernetes + Helm** — Used for deploying and managing the app at scale.

**Flow:**
```
User → Flask App → Boto3 → AWS EC2 → JSON Response
             │
             └──→ Docker → Helm → Kubernetes Deployment
```

---

## ⚙️ Technologies Used

| Category | Tools |
|-----------|-------|
| Language | Python 3 (Flask) |
| Cloud SDK | AWS Boto3 |
| Containerization | Docker |
| Orchestration | Kubernetes |
| Deployment | Helm |
| Infrastructure | AWS (EC2, IAM) |

---

## 🧰 Setup & Installation

### 1️⃣ Clone the Repository
```bash
git clone https://github.com/Jacob14meju/flask-aws-monitor.git
cd flask-aws-monitor
```

### 2️⃣ Build Docker Image
```bash
docker build -t flask-aws-monitor .
```

### 3️⃣ Configure AWS Credentials
Before running, make sure you have valid AWS credentials set up (via environment variables or `~/.aws/credentials`):
```bash
export AWS_ACCESS_KEY_ID=<YOUR_KEY>
export AWS_SECRET_ACCESS_KEY=<YOUR_SECRET>
```

### 4️⃣ Run Locally
```bash
python app.py
```
or with Docker:
```bash
docker run -p 5000:5000 flask-aws-monitor
```

### 5️⃣ Deploy with Helm to Kubernetes
```bash
helm install aws-monitor ./helm
```

---

## 📊 Example Output

When running, the Flask app will print information about active EC2 instances, such as:
```json
[
  {
    "InstanceId": "i-0abcd1234ef567890",
    "InstanceType": "t3.medium",
    "State": "running",
    "Region": "eu-central-1"
  }
]
```

---

## 🧠 Key Learning Goals

- Working with AWS APIs programmatically using **Boto3**
- Building a full deployment lifecycle: Flask → Docker → Kubernetes → Helm
- Infrastructure automation and scalability
- DevOps mindset: combining software and cloud engineering

---

## 🧑‍💻 Author

**Jacob Meju**  
DevOps Engineer | Cloud & Infrastructure Automation  
📧 mejuboygamer@gmail.com  
🔗 [LinkedIn](https://www.linkedin.com/in/jacob-mejubovsky-993b8a30a)  
💻 [GitHub](https://github.com/Jacob14meju)

---

## ⭐ Future Improvements

- Add AWS CloudWatch metrics dashboard  
- Integrate with Prometheus & Grafana for live monitoring  
- Add CI/CD pipeline via GitHub Actions  
- Extend to support multiple AWS services (S3, RDS, Lambda)

---

## 📄 License
MIT License — free to use and modify.
