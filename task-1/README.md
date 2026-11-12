# Task 1: Continuous Integration (CI) Pipeline Breakdown
#### This directory contains the Python application, unit test suite, and container configuration validated by `.github/workflows/ci.yml`. 

## CI Workflow Line-by-Line Breakdown (`.github/workflows/ci.yml`)

<img width="577" height="760" alt="image" src="https://github.com/user-attachments/assets/04a906f7-6a55-457e-a16f-037c567884a1" />



### Workflow Setup & Triggers (ci.yml)


<img width="523" height="183" alt="image" src="https://github.com/user-attachments/assets/cbb20568-ade8-48fd-9cbb-f582db228e3f" />

* **`Name:` this is just the name of my automation workflow which I will see label for on my GitHub dashboard.**
* **`on`: keyword that defines the trigger events that tell the platform when to automatically run the workflow.**
* **`push`: runs the workflow when code is pushed to specific branches, tags or paths. In this case, I have chosen to push it to branches main or master which triggers the script to run automatically.**
* **`pull_request`: runs the workflow when a pull request is opened, synchronized or reopened against target branches. In this case, if I were to submit a pull request trying to merge code into main or master, it automatically runs the checks to make sure the code is safe before it is approved.**


#### Job configuration (Where it runs)

<img width="517" height="109" alt="image" src="https://github.com/user-attachments/assets/2ea9795b-0f7f-4256-bd1f-60ff4e1b9ca0" />


* **`jobs:` a workflow that can have one or many tasks and groups them together. can run jobs in parallel by default where they get executed at the same time or can configure to wait for one another.**
* **`runs-on:` specify the OS to host the job, in this case, I have chosen to use ubuntu. It is like GitHub is renting me a fresh brand-new virtual machine in the cloud running linux for a few minutes to the work and then binning it when it’s done. It is specific steps within the workflow script so downloading code files from GitHub, installing python, running the unit tests to ensure the math/code passes and building docker container image to make sure it compiles correctly.**
* **`build-and-test:` This is the custom name for this specific job.**

#### Pipeline steps (What it runs): 

<img width="586" height="120" alt="image" src="https://github.com/user-attachments/assets/83917276-477c-43bc-b521-37843acc12d1" />

* **`steps:` like a to-do list checklist which tell the cloud computer to do these actions one by one in exact order from top to bottom. Every item starting with a dash (-) is a single task on that list.**
* **`name:` just labelling that specific item on the to-do list so when GitHub runs the pipeline, can easily read what it’s currently doing. Just keeps it clean and readable when looking through logs.**
* **`uses:` import and run reusable pieces of code known as actions. Saves the time of having to write code from scratch.**
* **`actions/checkout` this is the exact name of the pre-made helper tool. Actions means it lives inside the GitHub’s official library of helper tools and checkout clones the code repository into the temporary virtual machine running my pipeline.** 
* **`v3` - Just the version number of tool. The version should be taken into consideration because it prevent the pipeline from breaking if the developers were to roll out an update with changes that are not ready to take effect within my pipeline.**


<img width="488" height="131" alt="image" src="https://github.com/user-attachments/assets/e153a88d-f393-4f47-911e-8e9ed1cd0484" />


* **`name:` name of the next item**
* **`uses:` another prebuilt helper tool which installs python on the temporary virtual machine.** 
* **`with:` uses these specific settings so I am telling it to install python 3.9**


<img width="778" height="147" alt="image" src="https://github.com/user-attachments/assets/9e48fed6-170c-4327-bf57-e88121374fe0" />

* **`name:` name of the item** 
* **`cd task-1:` enters the task 1 folder where the app and tests are stored**
* **`Python -m unittest discover -s tests:` commands python to automatically scan the tests folder, look for any unit test files and run them back to check if everything passes successfully.**
* Python – boots the python interpreter program. Telling python to wake up and get ready to scan some code 
* -m : stands for module and instructs python to run a library module as a script. When typing -m, python scans through installed packages to find the desired module to run. 
* Unittest – the built in testing library tool that reads, tests the math/code answers and match what is expected. Reports back whether everything had passed or not. 
* Discover – automated process where a testing framework or build tool scans your project directory to find files, tests or modules that need to be ran or built. In my use case, discover is telling python to go search through the folders automatically to spot any test files. 
* -s tests : -s stands for start directory. It tells python to scan straight for the folder named test and look there rather than spending time scanning node modules, virtual environments or documentation folders. 


<img width="513" height="175" alt="image" src="https://github.com/user-attachments/assets/bfb94443-ce13-4aa7-a2e0-95ca8f801d70" />


* **`name:` name of the item**
* **`run |` telling github to run the terminal commands one after another**
* **`cd task-1` - walks into task 1 folder as this is where all our code and files live like an office room. GitHub actions drops you off at the front door lobby. If we don’t run this command, commands like flake8 will not know where to find the files and crash.** 
* **`flake` - popular command line tool used to check the style and quality of my python code. It is a linter which scans my source code without running it to look for programmatic errors, bad practices, stylistic issues or syntax mistakes. It is an automated code reviewer that prevents bad or unreadable code from reaching production. Flake8 will fail the pipeline step if someone was to write messy code before it merges.** 
* **`pip install flake8:` downloads the linting tool onto the github runner.** 
* **`flake app/` - scans the app/ folder for any style or syntax mistakes.**



<img width="556" height="145" alt="image" src="https://github.com/user-attachments/assets/5c586637-cf5d-4022-aa5b-b8582f8aa197" />


* **`run:` tells GitHub to run the following terminal commands one after the other.** 
* **`cd task-1` - walks into the task 1 folder so it can find the Dockerfile.** 
* **`docker build` - main command that wakes up docker and tells it to look for a dockerfile and start putting a container image together.**
* **`-t` - The tag flag which simply puts a name the container. Do not have to put this but it better to add it for reference and easier to remember the container ID rather than a string of random letters and numbers.** 
* **`python-app` - giving it a human friendly name.** 
* **`latest` - tells anyone looking at it that it is the most current up to date version of this app.** 
* **`.` - tells docker where to look to find the docker file and project file. It means this current folder right here.** 
  

