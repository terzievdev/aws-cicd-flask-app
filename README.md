# AWS CI/CD Flask API Pipeline 🚀

Automated CI/CD pipeline using GitHub Actions, Docker, AWS ECR, and EC2.

## 🏗️ Architecture
```
GitHub Push → GitHub Actions → Docker Build → AWS ECR → EC2 Deployment
```

## 🛠️ Technologies

- **Python Flask** - REST API framework
- **Docker** - Containerization
- **GitHub Actions** - CI/CD automation
- **AWS ECR** - Container registry
- **AWS EC2** - Application hosting
- **Gunicorn** - WSGI HTTP Server

## 📦 Features

- Automated build and deployment on push to main branch
- Docker containerization for consistency
- AWS ECR for secure image storage
- Zero-downtime deployments
- Health check endpoint

## 🚀 API Endpoints

- `GET /` - Welcome message with status
- `GET /health` - Health check endpoint

## 🔧 Setup Instructions

### Prerequisites

- AWS Account
- GitHub Account
- AWS CLI configured
- Docker installed on EC2

### AWS Resources Created

1. **ECR Repository**: `flask-api`
2. **EC2 Instance**: `flask-api-server` (t2.micro)
3. **IAM User**: `github-actions-user`
4. **IAM Role**: `EC2-ECR-Access-Role`
5. **Security Group**: HTTP (80), Custom TCP (5000), SSH (22)

### GitHub Secrets Required

- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`
- `EC2_HOST`
- `EC2_SSH_KEY`

## 📊 Deployment Process

1. Developer pushes code to `main` branch
2. GitHub Actions workflow triggers
3. Docker image builds from Dockerfile
4. Image tagged with commit SHA and `latest`
5. Image pushed to AWS ECR
6. SSH connection to EC2 instance
7. Deploy script pulls latest image
8. Old container stopped, new container started
9. Application accessible on port 80

## 🧪 Testing
```bash
# Test main endpoint
curl http://<EC2-PUBLIC-IP>/

# Test health endpoint
curl http://<EC2-PUBLIC-IP>/health
```

## 📁 Project Structure
```
aws-cicd-flask-app/
├── .github/
│   └── workflows/
│       └── deploy.yml       # GitHub Actions workflow
├── app.py                   # Flask application
├── Dockerfile               # Docker image definition
├── requirements.txt         # Python dependencies
├── .gitignore              # Git ignore rules
└── README.md               # This file
```

## 🔐 Security Considerations

- IAM user with minimal required permissions
- EC2 instance with IAM role (no hardcoded credentials)
- Private ECR repository
- Security group rules restrict access
- SSH keys never committed to repository

## 🎯 Skills Demonstrated

- **CI/CD**: GitHub Actions workflow automation
- **Containerization**: Docker multi-stage builds
- **Cloud Services**: AWS ECR, EC2, IAM
- **Infrastructure**: Security Groups, IAM Roles
- **Scripting**: Bash deployment scripts
- **API Development**: RESTful API with Flask

## 📈 Future Improvements

- [ ] Add automated testing in CI pipeline
- [ ] Implement blue-green deployment
- [ ] Add monitoring and logging (CloudWatch)
- [ ] Set up Application Load Balancer
- [ ] Add environment variables management
- [ ] Implement database integration
