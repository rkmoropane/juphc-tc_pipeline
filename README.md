# Intro to CI/CD Practice Code

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Python 3.9](https://img.shields.io/badge/Python-3.9-green.svg)](https://shields.io/)

This repository contains the practice code for the labs in **IBM-CD0215EN-SkillsNetwork Introduction to CI/CD**

## Contents

- Lab 1: [Build an empty Pipeline](labs/01_base_pipeline/README.md)
- Lab 2: [Adding GitHub Triggers](labs/02_add_git_trigger/README.md)
- Lab 3: [Use Tekton CD Catalog](labs/03_use_tekton_catalog/README.md)
- Lab 4: [Integrate Unit Test Automation](labs/04_unit_test_automation/README.md)
- Lab 5: [Building an Image](labs/05_build_an_image/README.md)
- Lab 6: [Deploy to Kubernetes](labs/06_deploy_to_kubernetes/README.md)

## Instructor

John Rofrano, Senior Technical Staff Member, DevOps Champion, @ IBM Research

## <h3 align="center"> © IBM Corporation 2022. All rights reserved. <h3/>

# IBM Full Stack JavaScript Certificate  
## Course 6: Cloud Native, DevOps, Agile, and NoSQL  
### Final Project: Tax Calculator CI/CD Pipeline

---

## 📌 Project Overview

This project is part of the IBM Full Stack JavaScript Certificate.  
It demonstrates how to modernize a simple **Tax Calculator application** using:

- Docker containerization
- Unit testing with Jasmine
- CI/CD pipelines using Tekton
- IBM Cloud Code Engine deployment
- IBM Container Registry
- Kubernetes secrets and resources

The final result is a fully automated **Cloud Native DevOps pipeline**.

---

## 🎯 Project Objectives

- Containerize a web application using Docker
- Run automated unit tests
- Build a CI/CD pipeline using Tekton
- Push Docker images to IBM Container Registry
- Deploy application to IBM Cloud Code Engine
- Automate build, test, and deployment steps

---

## 🧰 Tools & Technologies

- Docker
- Node.js
- Jasmine (Unit Testing)
- IBM Cloud CLI (`ibmcloud`)
- IBM Code Engine
- IBM Container Registry (ICR)
- Kubernetes (`kubectl`)
- Tekton Pipelines (`tkn`)
- Git & GitHub

---

## 📁 Project Structure

```text
zntwk-tax_calculator/
│
├── index.html
├── script.js
├── style.css
├── Dockerfile
├── package.json
├── spec/ (Jasmine tests)
└── README.md
```

---

## 🚀 Step-by-Step Implementation

# 1. Clone Repository

```bash
cd /home/project
git clone https://github.com/ibm-developer-skills-network/zntwk-tax_calculator.git
cd zntwk-tax_calculator
```

---

# 2. Run Application Locally

```bash
python3 -m http.server
```

Open browser:
```
http://localhost:8000
```

---

# 3. Run Unit Tests (Jasmine)

```bash
npm install
npx jasmine
```

Expected output:

```text
7 specs, 0 failures
```

---

# 4. Containerize Application (Docker)

## Dockerfile

```dockerfile
FROM nginx

COPY index.html /usr/share/nginx/html/
COPY script.js /usr/share/nginx/html/
COPY style.css /usr/share/nginx/html/
```

## Build Image

```bash
docker build -t tax-calculator .
```

## Run Container

```bash
docker run -dp 8080:80 tax-calculator
```

Open:

```
http://localhost:8080
```

---

## 5. Push Image to IBM Container Registry

```bash
docker tag tax-calculator us.icr.io/${SN_ICR_NAMESPACE}/tax-calculator

docker push us.icr.io/${SN_ICR_NAMESPACE}/tax-calculator
```

---

## 6. Deploy to IBM Code Engine

```bash
ibmcloud ce application create \
  --name tax-calculator \
  --image us.icr.io/${SN_ICR_NAMESPACE}/tax-calculator \
  --registry-secret icr-secret \
  --port 80
```

Get application URL:

```bash
ibmcloud ce application get --name tax-calculator
```

Example URL:

```
https://tax-calculator.<random>.codeengine.appdomain.cloud
```

---

## 7. Create Kubernetes Secret

```bash
kubectl create secret docker-registry docker-reg-creds \
  --docker-server=us.icr.io \
  --docker-username=iamapikey \
  --docker-password=$IBMCLOUD_API_KEY
```

---

## 8. CI/CD Pipeline (Tekton)

### Pipeline Tasks

- `npminstall` → installs dependencies
- `jasmine` → runs unit tests
- `buildah` → builds and pushes Docker image

---

## 9. Run Pipeline

```bash
kubectl apply -f tasks.yaml
kubectl apply -f pipeline.yaml
kubectl create -f run.yaml
```

---

## 10. Monitor Pipeline

```bash
tkn pipelinerun logs --last
```

---

## 🌐 Final Deployment

The application is deployed on IBM Cloud Code Engine:

👉 **Live URL:**
```
https://tax-calculator.2beo6vdzhsb1.us-south.codeengine.appdomain.cloud
```

---

## 📊 Key Concepts Learned

### ✔ DevOps Pipeline
Automates build → test → deploy workflow.

### ✔ Containerization
Application packaged using Docker for portability.

### ✔ Unit Testing
Jasmine ensures code correctness before deployment.

### ✔ Cloud Deployment
IBM Code Engine runs the application serverless.

### ✔ CI/CD Automation
Tekton pipelines handle full lifecycle automation.

---

## 🔐 Important Commands

```bash
ibmcloud ce application list
ibmcloud ce application get --name tax-calculator
tkn pipelinerun list
kubectl get pods
```

---

## 🏁 Conclusion

This project demonstrates a complete **Cloud Native DevOps workflow**:

- Code → Test → Build → Deploy → Run
- Fully automated pipeline
- Cloud-hosted application

You now have hands-on experience with real-world DevOps practices used in modern software engineering.

---

## 👨‍💻 Author

IBM Skills Network Lab Project  
Course: IBM Full Stack JavaScript Developer  