# 🚗 Vehicle Insurance Prediction using MLOps

A complete end-to-end MLOps project designed to predict vehicle insurance policies with production-ready CI/CD pipelines, cloud storage, and modular architecture. This project combines the best practices of machine learning, software engineering, and DevOps.

---

## 📌 Project Highlights

- 🧰 Modular Python package with `setup.py` and `pyproject.toml`
- 🧪 Virtual environment and dependency management with `conda` and `requirements.txt`
- 📊 Comprehensive EDA & Feature Engineering
- ⚙️ Component-based architecture: Data Ingestion, Validation, Transformation, Model Training, Evaluation & Pushing
- ☁️ AWS Integration (S3, IAM, EC2, ECR)
- 🐳 Dockerized CI/CD pipeline using GitHub Actions and Self-Hosted Runner on EC2
- 🌍 Deployed Flask app accessible via public IP and port

---

## 🧱 Project Structure

```
├── app.py                       # Flask API entry point
├── notebook/                   # EDA & initial MongoDB data push
├── src/
│   ├── components/             # ML pipeline components (ingestion, validation, training, etc.)
│   ├── configuration/          # MongoDB & AWS connection handlers
│   ├── data_access/            # MongoDB data fetch logic
│   ├── entity/                 # Config & Artifact entity classes
│   ├── exception.py            # Custom exception handling
│   ├── logger.py               # Logging setup
│   ├── aws_storage/            # AWS S3 push/pull handlers
│   └── utils/                  # Helper functions and schema definitions
├── .github/workflows/          # GitHub Actions workflow YAML
├── Dockerfile                  # Docker image setup
├── requirements.txt            # Project dependencies
├── setup.py                    # Local package setup
├── pyproject.toml              # Build configuration
└── .gitignore
```

---

## 🚀 Getting Started

### 🧪 Create & Setup Environment

```bash
conda create -n vehicle python=3.10 -y
conda activate vehicle
pip install -r requirements.txt
```

Verify with:
```bash
pip list
```

### ⚙️ Local Package Setup

```bash
python template.py
```

Configure `setup.py` and `pyproject.toml` to enable local package imports.  
Refer `crashcourse.txt` for packaging structure info.

---

## 🧩 Component Pipeline

Each ML pipeline stage is isolated in `src/components`.

### 🔹 Data Ingestion

- Setup DB connection in `configuration.mongo_db_connection.py`
- Define config and artifact classes
- Build ingestion logic in `components.data_ingestion.py`
- Trigger from `demo.py`

Set MongoDB URI as environment variable:

```bash
# Bash
export MONGODB_URL="your_mongo_url"

# PowerShell
$env:MONGODB_URL="your_mongo_url"
```

---

### 🔹 Data Validation & Transformation

- Define schema in `config/schema.yaml`
- Implement logic in `components.data_validation.py` and `components.data_transformation.py`
- Add transformation classes in `entity/estimator.py`

---

### 🔹 Model Trainer

- Add logic to train and save models
- Implemented in `components/model_trainer.py` and `entity/estimator.py`

---

## ☁️ AWS Integration

### 🔐 IAM Setup

- Create IAM user (`firstproj`) with `AdministratorAccess`
- Generate access keys and set as environment variables:

```bash
# Bash
export AWS_ACCESS_KEY_ID=...
export AWS_SECRET_ACCESS_KEY=...

# PowerShell
$env:AWS_ACCESS_KEY_ID="..."
$env:AWS_SECRET_ACCESS_KEY="..."
```

- Define variables in `constants/__init__.py`
- Create S3 Bucket: `my-model-mlopsproj19`
- Add AWS handling logic in `aws_storage/` and `entity/s3_estimator.py`

---

### 🔍 Model Evaluation & Deployment

- Set threshold in `constants/__init__.py`
- Create ModelEvaluation and ModelPusher components
- Add prediction logic in `app.py`
- Setup frontend in `static/` and `templates/`

---

## 🔄 CI/CD with Docker, GitHub Actions & EC2

### 🐳 Docker & GitHub Actions

- Create `Dockerfile` and `.dockerignore`
- Define GitHub workflow YAML in `.github/workflows/aws.yaml`

### 📦 AWS ECR & EC2

- Create ECR repo: `vehicleproj`
- Launch EC2 (Ubuntu 24.04, T2 Medium)
- Install Docker:

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker ubuntu
newgrp docker
```

### 🧑‍💻 Self-Hosted Runner

- Register EC2 as GitHub self-hosted runner
- Follow GitHub’s instructions to configure and run

### 🔐 GitHub Secrets

Set in GitHub > Settings > Secrets:

- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`
- `AWS_DEFAULT_REGION`
- `ECR_REPO`

---

## 🌐 Accessing the App

1. Allow port 5080 in EC2 Inbound rules
2. Visit:
```bash
http://<ec2-public-ip>:5080
```

3. Use `/training` endpoint to trigger training

---

## 💡 Tech Stack

| Tool/Service | Purpose |
|--------------|---------|
| Python       | Core development |
| MongoDB Atlas| Database |
| AWS S3       | Model storage |
| Docker       | Containerization |
| GitHub Actions | CI/CD |
| EC2          | Deployment |
| ECR          | Docker registry |
| Flask        | Web API |
| Conda        | Environment |
| Jupyter      | EDA & Prototyping |

---

## 📈 Future Enhancements

- Add monitoring (Prometheus/Grafana)
- Integrate DVC for data versioning
- Add unit testing for robustness
- Use multi-stage Docker builds for optimization

---

## 🤝 Connect with Me

📧 atulyaverma7068@gmail.com  
🔗 [LinkedIn](https://www.linkedin.com/in/atulyaverma02/)  
💻 [GitHub](https://github.com/Atulyaverma70)

---

> *This repository showcases the real-world application of MLOps and cloud deployment using best practices and industry tools.*