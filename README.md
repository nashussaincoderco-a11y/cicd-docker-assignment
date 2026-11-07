# CI/CD Containerised Python Application
#### This is an end to end project I built demonstrating how to utilise continuous integration and continuous deployment workflows using GitHub Actions and Docker Hub.
#### With this sort of workflow, you are easily able to automate testing and deployment simply using 2 main tools which are GitHub actions and Docker Hub. 


## What This Project Does: 
Whenever code is pushed top the main branch, automated workflows run to:
1. **Tests the code**: Runs automatic unit tests to make sure everything works.
2. **Build & Deploy**: Packages the Python application into a Docker Container and uploads it directly to Docker Hub.


## Key features and tools used for this project: 
-  **Automated Testing**: Runs Pytest suites across commits via GitHub Actions
-  **Containerization** : Packs the Python application into a lightweight Docker Image
-  **Continuous Deployment**: Automatically builds and pushes updated images to Docker Hub.
-  **Secure Secret Management**: Utilises GitHub Repository secrets for Docker API Authentication.

## 📁 Repository Structure

```text
cicd-docker-assignment/
├── .github/
│   └── workflows/
│       ├── ci.yml          # Task 1: Continuous Integration Pipeline (Automated testing)
│       └── deploy.yml      # Task 2: Continuous Deployment Pipeline (Automated deployment)
├── task-1/
│   ├── app/
│   │   └── main.py         # Python Application code & logic
│   ├── tests/
│   │   └── test_main.py    # Unit tests
│   ├── Dockerfile          # Container build instructions
├── task-2/
```


<img width="509" height="330" alt="image" src="https://github.com/user-attachments/assets/b88f89fb-4c9a-40e8-8e15-235158e350a2" />



## Pipeline Architecture 
```
[ Push Code ] ──> [ GitHub Repository ]
                        │
       ┌────────────────┴────────────────┐
       ▼                                 ▼
[ CI Workflow ]                   [ CD Workflow ]
 ├── Checkout Code                 ├── Checkout Code
 ├── Setup Python                  ├── Docker Login (Secrets)
 ├── Install Dependencies          ├── Build Docker Image
 └── Run Unit Tests (pytest)       └── Push Image to Docker Hub
                                         │
                                         ▼
                             [ Docker Hub Registry ]
```


## How it works & implementation details:


#### Task 1: Continuos Integration

* File location: ```.github/workflows/ci.yml```
* What it does: Whenever code changes are pushed



