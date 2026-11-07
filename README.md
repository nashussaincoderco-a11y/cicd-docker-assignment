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
-  **Secure Secret Management**:
