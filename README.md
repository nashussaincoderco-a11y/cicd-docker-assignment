# CI/CD Containerised Python Application
#### This is an end to end project I built demonstrating how to utilise continuous integration and continuous deployment workflows using GitHub Actions and Docker Hub.
#### With this sort of workflow, you are easily able to automate testing and deployment simply using 2 main tools which are GitHub actions and Docker Hub. 


## What This Project Does: 
This project consists of 2 tasks and here is what happens, whenever code is pushed top the main branch, automated workflows run to:
1. **Test the code**: Runs automatic unit tests to make sure everything works.
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


Each directory represents a focused pipeline with its own code and documentation. 

All GitHub Actions workflows live in ```.github/workflows``` as this is the repository root required for GitHub actions. 

## How it works & implementation details:


### Task 1: Continuos Integration(CI)

* File location: ```.github/workflows/ci.yml```
* What it does: Whenever code changes are pushed, GitHub sets up Python, installs dependencies and runs unit tests using ```pytest``` to catch bugs early.
* * <a href="[https://github.com/nashussaincoderco-a11y/cicd-docker-assignment/tree/main/task-1](https://github.com/nashussaincoderco-a11y/cicd-docker-assignment/tree/main/task-1)" target="_blank">Click here to view my step-by-step implementation</a>



### Task 2: Continuous Development(CD) 
* File location: ```.github/workflows/deploy.yml```
* Docker Hub Registry: nashussaincoderco/python-app
* What it does: Automatically logs into Docker Hub using secure secrets, builds the Docker image from your Docker file, and pushes the latest version live.
* [Click here to view my step by step implementaion](https://github.com/nashussaincoderco-a11y/cicd-docker-assignment/tree/main/task-2). 



### Screenshots of Pipeline Passing for Task 1: 


#### The Workflow Run Dashboard


<img width="940" height="295" alt="image" src="https://github.com/user-attachments/assets/fbab7a67-cd1e-4be2-8d32-62d6fc6085a8" />


As you can see on the screenshot above, it displays the successful execution of the continuous integration workflow on GitHub actions following a code push to the main branch. It confirms the pipeline's status, matching commit details and total runtime duration with a passing green check mark indicator.  


#### For the Job Execution Step Breakdown 


<img width="940" height="417" alt="image" src="https://github.com/user-attachments/assets/af47aec1-dda6-4489-a953-ed832411e9ed" />


The detailed log above breaks down the individual stages of the build-and-test job. It verifies that the environment setup, unit testing, code linting and Docker image compilation steps all completed successfully in sequence. 


### Screenshots of Pipeline passing for Task 2: 



<img width="940" height="369" alt="image" src="https://github.com/user-attachments/assets/e8fa0c40-ab1c-4c11-8419-bb29e95baf26" />


As you can see on the Dashboard view, it shows the successful execution of the automated continuous deployment (CD Pipeline) workflows on GitHub actions which confirms that the code pushes to the main branch triggered the deployment process properly with passing green indicators. 



<img width="1852" height="768" alt="image" src="https://github.com/user-attachments/assets/ed6f73a2-695d-4248-bafc-c49ddbe05bb4" />


This detailed log highlights the execution steps of the build-and-deploy job illustrating how the pipeline securely authenticates with Docker Hub. It compiles and pushes the container image and completes the deployment sequence successfully. 


<img width="940" height="168" alt="image" src="https://github.com/user-attachments/assets/6571a989-683a-44e7-869e-d7e34174f877" />


As you can now see on Docker Hub registry that it showcases the live availability of the published container under the nashussaincoderco/python-app namespace which confirms that the automated deployment successfully the latest image. 


## CI Optimization: Code Linting Order

You might have noticed earlier for my CI pipeline, I had set the workflow to build the docker image before initiating linting. I had noticed that if I let it stayed set to this, it will waste resources and time building containers if the pipeline was to fail. It can also lead to many other issues such as producing broken image builds, overloading my DockerHub repository with non-functional images and accidentally produce broken image builds. 



By having linting put in place before building docker images, it will check for quality and syntax issues before spending the compute time packaging the resources for the application into an image. So if the code linting was to fail, the pipeline stops immediately instead of building a broken container. 


<img width="940" height="824" alt="image" src="https://github.com/user-attachments/assets/e48c3c08-e915-4574-a9b1-705f319afddf" />

As you can see on the screenshot above, I have set the linting step before the docker image build. Once I made that change, I ran a git commit and push to upload the changes to my GitHub. 


<img width="940" height="302" alt="image" src="https://github.com/user-attachments/assets/a23907a7-41bb-4d96-a9fa-e7afd6cf4949" />


You can see that it displays a successful execution of the CI pipeline ```(ci.yml)``` triggered by a commit on the main branch which confirms the build-and-test job passed successfully indicated by the green tick. 


<img width="940" height="367" alt="image" src="https://github.com/user-attachments/assets/f7366d1a-8cfd-4c9d-b0fe-f794c1debf25" />


You can now see that when I click to view the logs, it confirms the CI execution order demonstrating that the code Linting stage runs before the docker image build. This enforces the fail-fast approach because it validates code formatting before initiating the container compilation step. 























