# Task 2: CD - Automated Docker Build & Registry Push (deploy.yml)

## Overview: This workflow automates Continuous Delivery (CD) by building Docker image and pushing it to a container registry whenever changes are merged into the main branch. 


### GitHub Secrets & Secure Authentication 




<img width="940" height="498" alt="image" src="https://github.com/user-attachments/assets/077b3a48-1d20-408a-b4b2-2244cc2f606a" />


To let GitHub Actions push the Docker image automatically without exposing my login details, I stored my Docker Hub credentials as encrypted repository secrets. This allows: 
* `Secure Authentication:` It enables the automated GitHub actions pipeline to log into the DockerHub securely without exposing my credentials in plain text inside the workflow code.
* `Protecting Sensitive Data:` Keeping access tokens encrypted as repository secrets prevents anyone visiting my GitHub repository or stealing the login keys.
* `Hands-free Automation:` The pipeline automatically pulls these hidden credentials during the build-and-push step allowing the Continuous Delivery (CD) workflow run automatically whenever the code is updated.  



## Continuous Delivery (CD) Breakdown (.github/workflows/deploy.yml): 


<img width="940" height="601" alt="image" src="https://github.com/user-attachments/assets/fab0f460-d8c7-4c93-b6be-827ef7c34560" />


### Workflow Setup & Triggers (deploy/yml): 


<img width="364" height="136" alt="image" src="https://github.com/user-attachments/assets/26674cb3-df32-4b04-84b1-349af5a3742e" />

* **`name:` Setting the display name of the workflow for when it appears under the actions tab on GitHub.** 
* **`on:` specifies the trigger events that tell the automation platform when to execute the workflow. Tells github when to run this workflow.**
* **`push:` specifies that the workflow should trigger automatically whenever code is pushed.** 
* **`branches: [ main ]` – restricts the trigger so it only runs when pushes are made specifically to my main branch. Without this, the workflow would run every single time anyone pushed code to any branch in the entire repository.**


### Job configuration (Where it runs): 


<img width="304" height="65" alt="image" src="https://github.com/user-attachments/assets/cca7ac67-cd09-4ace-b35c-9024f56da29e" />


* **`jobs:` Groups together all the tasks that need to run in this workflow.**
* **`build-and-deploy:` the unique ID name given to this specific job list.** 
* **`runs-on:` ubuntu-latest = Tells Github actions to spin up a clean fresh cloud environment running Ubuntu Linux to execute my pipeline steps.**


### Pipeline steps (What it runs): 

<img width="341" height="77" alt="image" src="https://github.com/user-attachments/assets/19413276-0d84-4a73-a995-b39f01e58136" />


* **`Steps:` a sequential list of tasks the virtual machine will initiate one after the other. Like a step-by-step instruction the computer executes from top to bottom. 
* **`name:` just a name label for this specific step. 
* **`uses: actions/checkout@v3` – a pre-build GitHub tool that downloads my repository code onto the virtual machine so the pipeline can see and use my files.


<img width="501" height="101" alt="image" src="https://github.com/user-attachments/assets/d0f972b3-ab88-4420-83a0-2a7bc9de2ea3" />



* **`name:` a readable name for the authentication step** 
* **`uses: docker/login-action@v2` – a pre-built Github action used to log into docker registry such as Docker Hub, GitHub packages and AWS ECR.** 
* **`with:` tell GitHub how to use the tool within this step. I type in the choices I want to login to Docker Hub. I’ve put username and password for the docker registry so it will only send that data to GitHub actions.** 
* **`username: ${{ secrets.DOCKER_USERNAME }}` – safely grabs my saved DOCKER_USERNAME repository secret without exposing my actual username in plain text code.**
* **`password: ${{ secrets.DOCKER_PASSWORD }}` – safely grabs the encrypted Docker Hub access token secret to authenticate securely.**


<img width="863" height="216" alt="image" src="https://github.com/user-attachments/assets/5892d40b-28b7-46b9-9e01-1c670a41e015" />


* **`name:` Build and push docker image – just a name label for this specific step.** 
* **`run: |` will run commands that will be executed within this step. It tells the virtual machine to run standard terminal shell commands line by line.** 
* **`cd task-1 :` switches to the terminal path into the task-1 directory where the DockerFile and python application live inside.**  
* **`Docker build -t nashussaincoderco/python-app:latest :` builds the docker image, tags it with -t with my DockerHub username (nashussaincoderco/python-app:latest) and builds it using my current folder with the (.). Docker Build is the command that takes my source code and docker file then packages them together into a docker image.** 
* **`docker push nashussaincoder/python-app:latest :` uploads that newly docker built container image from GitHub straight up to my cloud Docker Hub account registry.** 















