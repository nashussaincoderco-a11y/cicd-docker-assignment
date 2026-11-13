# Task 2: CD - Automated Docker Build & Registry Push

## Overview: This workflow automates Continuous Delivery (CD) by building Docker image and pushing it to a container registry whenever changes are merged into the main branch. 


## GitHub Secrets & Secure Authentication 


<img width="940" height="498" alt="image" src="https://github.com/user-attachments/assets/077b3a48-1d20-408a-b4b2-2244cc2f606a" />


To let GitHub Actions push the Docker image automatically without exposing my login details, I stored my Docker Hub credentials as encrypted repository secrets. This allows: 
* `Secure Authentication:` It enables the automated GitHub actions pipeline to log into the DockerHub securely without exposing my credentials in plain text inside the workflow code.
* `Protecting Sensitive Data:` Keeping access tokens encrypted as repository secrets prevents anyone visiting my GitHub repository or stealing the login keys.
* `Hands-free Automation:` The pipeline automatically pulls these hidden credentials during the build-and-push step allowing the Continuous Delivery (CD) workflow run automatically whenever the code is updated.  


