[![CI/CD Pipeline Status](https://github.com/ashaduzzaman-sarker/MLOps-Production-Ready-Machine-Learning-Project-Wine-Quality-Prediction/actions/workflows/cicd.yaml/badge.svg)](https://github.com/ashaduzzaman-sarker/MLOps-Production-Ready-Machine-Learning-Project-Wine-Quality-Prediction/actions/workflows/cicd.yaml)

# MLOps-Production-Ready-Machine-Learning-Project_Wine_Quality_Prediction

This repository implements a production-ready MLOps pipeline for predicting wine quality. It integrates modular code, pipeline automation, and deployment, following best practices for machine learning and software engineering. The project includes data ingestion, validation, transformation, model training, evaluation, and deployment using Flask and AWS.

## **Table of Contents**
1. [Project Overview](#project-overview)
2. [Features](#features)
3. [Directory Structure](#directory-structure)
4. [How to Run](#how-to-run)
5. [CICD Deployment](#aws-cicd-deployment-with-github-actions)
6. [Technologies Used](#technologies-used)
7. [Contributing](#contributing)
8. [License](#license)


## **Project Overview**
The **Wine Quality Prediction** project predicts the quality of wine based on its chemical properties. The project:
- Ingests data from raw files.
- Validates and preprocesses the data.
- Trains a machine learning model.
- Evaluates model performance.
- Serves the model via a REST API.

The project follows a robust MLOps structure and leverages CI/CD pipelines for automated testing, deployment, and monitoring.


## **Features**
- **Data Pipelines**: Automated ingestion, validation, and transformation.
- **Configurable**: Easily customizable through YAML configuration files.
- **Model Training**: Modularized training pipeline with evaluation and logging.
- **API Deployment**: Flask-based API for predictions.
- **CI/CD Integration**: GitHub Actions for deployment and testing.
- **AWS Deployment**: Dockerized application deployed using EC2 and ECR.


## **Directory Structure**

```plaintext
mlops_project/
├── .github/workflows/        # CI/CD workflows
│   └── cicd.yaml
├── config/                   # Configuration files
│   ├── config.yaml
│   ├── schema.yaml
│   ├── params.yaml
├── research/                 # Notebooks for EDA and experimentation
│   ├── 00_EDA.ipynb
│   ├── 01_data_ingestion.ipynb
│   ├── 02_data_validation.ipynb
│   ├── 03_data_transformation.ipynb
│   ├── 04_model_trainer.ipynb
│   ├── 05_model_evaluation.ipynb
├── src/mlProject/            # Core project code
│   ├── components/           # Pipeline components
│   ├── config/               # Configuration management
│   ├── constants/            # Constants
│   ├── entity/               # Configuration entities
│   ├── pipeline/             # Pipeline stages
│   ├── utils/                # Utility functions
├── static/                   # Static files for API UI
│   ├── assets/
│   ├── css/
│   ├── js/
│   ├── templates/
├── Dockerfile                # Docker configuration
├── app.py                    # Flask application
├── main.py                   # Pipeline entry point
├── README.md                 # Documentation
├── requirements.txt          # Dependencies
├── setup.py                  # Package setup
└── test.py                   # Unit tests
```


## **How to Run**

### **Step 1: Clone the Repository**
```bash
git clone https://github.com/entbappy/End-to-End-Wine-Quality-Prediction
cd End-to-End-Wine-Quality-Prediction
```

### **Step 2: Set Up Environment**
Create a Python environment and install dependencies.

```bash
conda create -n mlproj python=3.8 -y
conda activate mlproj
pip install -r requirements.txt
```

### **Step 3: Run the Application**
Start the Flask app to serve predictions.
```bash
python app.py
```


## **AWS CICD Deployment with GitHub Actions**

### **1. AWS Setup**
- **IAM User**: Create a user with `AmazonEC2FullAccess` and `AmazonEC2ContainerRegistryFullAccess`.
- **ECR Repository**: Create an ECR repository to store Docker images.
- **EC2 Instance**: Launch an EC2 instance (Ubuntu) to host the application.

### **2. Dockerize the Application**
Build and push the Docker image to the ECR repository.
```bash
docker build -t wine-quality-app .
docker tag wine-quality-app:latest <your-ecr-uri>/wine-quality-app:latest
docker push <your-ecr-uri>/wine-quality-app:latest
```

### **3. Configure CI/CD**
Set up GitHub secrets for:
- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`
- `AWS_REGION`
- `AWS_ECR_LOGIN_URI`
- `ECR_REPOSITORY_NAME`

### **4. Self-Hosted Runner**
Set up an EC2 instance as a GitHub Actions runner:
```bash
# Update and install Docker
sudo apt-get update -y
sudo apt-get upgrade -y
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker ubuntu
```

### **5. Run CI/CD Workflow**
Push changes to trigger the CI/CD pipeline in GitHub Actions.


## **Technologies Used**
- **Python**: Core programming language.
- **Flask**: REST API framework.
- **Pandas, Scikit-Learn**: Data processing and ML.
- **Docker**: Containerization.
- **AWS**: Deployment platform (EC2, ECR).
- **GitHub Actions**: CI/CD pipeline.


## **Contributing**
Contributions are welcome! Please fork the repository and submit a pull request with your changes.


## **License**
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
