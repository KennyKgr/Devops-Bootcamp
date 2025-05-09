# Elite Corporation NGINYA Fintech App CI/CD Pipeline

## Project Structure
The project is organized into the following directory structure:

```
Nginya-fintech-app/
├── .github/workflows/
│   └── ci_cd_pipeline.yml
├── infrastructure/
│   ├── main.tf
│   ├── variables.tf
│   ├── outputs.tf
│   └── modules/    
│       ├── ec2/
│       │   └── main.tf
│       │   └── variables.tf
│       │   └── outputs.tf
│       ├── rds/
│       │   └── main.tf
│       │   └── variables.tf
│       │   └── outputs.tf
│       ├── lb/
│       │   └── main.tf
│       │   └── variables.tf
│       │   └── outputs.tf
│       └── ...
├── app/ app.js #Nginya fintech app source code
│   ├── ...
│   ├── tests/
│   │   └── ...
│   └── package.json
├── .env
├── README.md
└── ...

```
### Project Description
Elite Cooperation needed to build, test and deploy a new fintech app Named **Nginya** that had the following functionalities.
- Onboarding Clients
- Saving Money
- Trading in Stocks
- Buying Bitcoin with view of introducing other cryptocurriencies later on
- Send funds between users.
- Send money to other banks
- Send money to other countries

#### Project Requirements

- The project was to be built using **Node.js** and **Express.js** for the backend, with a **MongoDB database** for data storage.
- The project was to be containerized using **Docker**, with a CI/CD pipeline set up using **GitHub Actions** for continuous integration and deployment.
- The project was to be deployed on AWS using Terraform for infrastructure as code (IaC).
- The project was to be monitored using **AWS CloudWatch** and logs were to be stored in AWS S3.
- The project was to be secured using **AWS IAM roles** and policies, with access control implemented using **AWS Cognito**.
- The project was to be tested using **Jest** and **Supertest** for unit and integration testing.
- The Project was to be tested for vulnerabilities using **Snyk** and the code was to be scanned for vulnerabilities using **SonarQube**.
- The project was to be documented using Swagger and the documentation was to be hosted on GitHub Pages.
- The project use **Owasp ZAP** for security testing and the results were to be stored in **AWS S3**.


##### Project Setup

- I started by creating a directory called **fintech-app** to hold the project files and directories.

- Created a directory with 
  mkdir fintech-app
![filecreation](/Pj5/images/001_create_diectory_fintech_app.jpg)

- Cd into the fintech-app directory
![changedir](/Pj5/images/002_cd_into_fintech_app.jpg)

- Created the directories
![creation](/Pj5/images/003_create_the_various_directories.jpg)

- Cd into the github directory
![cdintothegithubdir](/Pj5/images/004_cd_into_.github_directory.jpg)

- Create the workflow directory
[createdworkflowdir](/Pj5/images/005_create_a_workflow_directory.jpg)

- Ran the sripts to initialize npm and install body parser with
```
  npm init -y

  npm install express body-parser`

```

![ran](/Pj5/images/007_install_body_parser.jpg)

- Created the index.js file with the command
```
  vi index.js
```
- I wrote my code in the index.js file with the following code
![code](/Pj5/images/008_created_index.js_wrote_my_code.jpg)

- I created a file called **.env** to store my environment variables

- I created a file called **.gitignore** to ignore the node_modules directory and the .env file
- I added the following lines to the .gitignore file:
```
node_modules/
.env
```
- I created a file called **ci.yml** in the .github/workflows directory to set up the CI/CD pipeline using GitHub Actions. The file contains the following code:
![createymlci](/Pj5/images/009_create_ci.yml_with_touch.jpg)

- input my code in the ci.yml file
![codeymlci](/Pj5/images/010_input_my_code_to_my_yml_file.jpg)

- Created a file called **cd.yml** in the .github/workflows directory to set up the CD pipeline using GitHub Actions.
![cdyml](/Pj5/images/011_create_a_cd.yml_file_and_input_the_configuration.jpg)

- Went into my terraform directory and created my Main.tf file with the command
```
  vi main.tf
```
- I wrote my code in the **main.tf** 
![main](/Pj5/images/012_create_my_main.tf_and_input_my_configuration.jpg)

- I created my **variables.tf** in the terraform directory to define the variables used in the main.tf file.
![variables](/Pj5/images/013_create_variable.tf_and_input_configurations.jpg)

- I created a file called **outputs.tf** in the terraform directory to define the outputs of the main.tf file.

- I Created my **terraform.tfvars** in the terraform directory to define the values of the variables used in the main.tf file.
![tfvars](/Pj5/images/014_create_terraform.tfvars_file_and_input_configuration.jpg)

- Set my github secrets with the following commands
```
  AWS_ACCESS_KEY_ID
  AWS_SECRET_ACCESS_KEY
  SYNK_TOKEN
```
![secrets](/Pj5/images/015_set_github_action_secrets.jpg)

- I initialized git in the fintech-app directory with the command
```
  git init
```
![gitinit](/Pj5/images/016_git_init.jpg)

- I added all the files to the git repository with the command
```
  git remote add origin
```
![gitremote](/Pj5/images/git_remote_add_origin.jpg)

- git add all the files to the git repository with the command
```
  git add .
```
![gitadd](/Pj5/images/018_git_add_dot.jpg)

- I did my initial commit with the files to the git repository with the command
```
  git commit -m "Initial commit"
```
![commit](/Pj5/images/019_git_commit_initial_commit.jpg)

- I created a new branch called **main** with the command
```
  git branch -M main
```
- Pushed to my repositosy with 
``
git push -u origin 
![push](/Pj5/images/020_git_push.jpg)

- My push was successful as I had files still loading in my repository
![pushok](/Pj5/images/021_push_successful.jpg)

- All tests and vulnerability scans carried out successfully
  
- I went to my github repository and checked the actions tab to see if my CI/CD pipeline was running and it was successful.
![jobrun](/Pj5/images/023_build_and_deploy_successful.jpg)

- Since my build and deploy was successful I went to aws to confirm and my resources were running

- Ec2 instance running
![aws](/Pj5/images/024_ec2_instance_created.jpg)

- Elastic Load Balancer created and running
- ![elb](/Pj5/images/025_load_balancer_also_created.jpg)

- RDS instance created and running

**END**