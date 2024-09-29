[![Python application test with Github Actions](https://github.com/toanla1306/udacity-azure-devops/actions/workflows/main.yml/badge.svg)](https://github.com/toanla1306/udacity-azure-devops/actions/workflows/main.yml)

# udacity-azure-devops
The lab of Azure Devops Project in Udacity course.



## Environment
Python 3.12 

# Overview

In this project, you’ll create a GitHub repository to establish a Continuous Integration (CI) and Continuous Delivery (CD) pipeline using GitHub Actions and Azure Pipelines. The setup includes a Makefile for managing build, test, and lint commands, a `requirements.txt` for dependency management, and your application code. CI will automate linting, testing, and installation on code pushes, while CD will facilitate deployment to Azure App Service, ensuring a streamlined workflow that enhances code quality and simplifies deployment for future projects.

## Project Plan

* [A link to a Trello board for the project](https://trello.com/b/lNaxDBtJ/azure-devops-udacity)
* [A link to a spreadsheet that includes the original and final project plan](https://docs.google.com/spreadsheets/d/1UiTmntfmnSDRe2zynKOoKIro_i-otHfnj2n09e-di6g/edit?usp=sharing)

## Instructions

Below are the Instructions on how to setup a CI/CD pipeline in Azure
![image](./screenshot/diagram.png)

## Project running on Azure App Service
- Create The MakeFile 
    ```
    install:
        pip3 install --upgrade pip &&\
            pip3 install -r requirements.txt

    test:
        python -m pytest -vv test_hello.py


    lint:
        pylint --disable=R,C hello.py

    all: install lint test
    ```
- Create the requirements.txt file
    ```
    flask==3.0.3
    pandas==2.2.2
    scikit-learn==1.5.1
    joblib==1.4.2
    pylint==3.2.6
    pytest==8.3.1
    ```
- Install all dependencies
    ```
    make all
    ```
- Start application and verify it is working well
    ```
    python app.py
    ```
-  Deploy application to Azure App Service
    ```
    az login
    az webapp up --name flask-ml-toanla --resource-group Azuredevops --runtime "PYTHON:3.12" --sku FREE
    ```
- Verify application run well in Azure App Service

    ![image](./screenshot/start-webapp-complete.png)

## Project cloned into Azure Cloud Shell
- Access the Console of Azure and Open the Azure Cloud shell
- Generate the SSH Key in this Cloud Shell 
    ```
    ssh-keygen
    cat ~/.ssh/id_sa.pub
    ```
- Copy the SSH Keygen to Github Repository
- Back to Console Azure Cloud Shell and clone your project

    ![image](./screenshot/azure_bash_clone_repo.png)

## Passing tests that are displayed after running the `make all` command from the `Makefile`
- Create the Makefile 
    ```
    install:
        pip3 install --upgrade pip &&\
            pip3 install -r requirements.txt

    test:
        python -m pytest -vv test_hello.py


    lint:
        pylint --disable=R,C hello.py

    all: install lint test
    ```
    ![image](./screenshot/run_makefile_local.png)

## Output of a test run
- Screenshot application is running well in localhost

    ![image](./screenshot/output_test_run_localhost.png)

## Successful deploy of the project in Azure Pipelines.  
[Note the official documentation should be referred to and double checked as you setup CI/CD](https://docs.microsoft.com/en-us/azure/devops/pipelines/ecosystems/python-webapp?view=azure-devops).

- Access the Cloud Shell and Generate SSHKeygen

    ![image](./screenshot/generate-sshkey.png)
- Clone Repository Application

    ![image](./screenshot/clone-repo-complete.png)

- Deploy application to Azure App Service

    ![image](./screenshot/deploy-application-azure-app-svc.png)

- Azure App Service Verification
    - Azure Service App Running
    
        ![image](./screenshot/application-in-azure-app-svc.png)

    - Access via Domain of App Service

        ![image](./screenshot/access-domain-app-svc.png)

- Initialization Azure Devops Workspace
    - Init Workspace

        ![image](./screenshot/init-new-workspace-az-devops.png)

    - Create Workspace with Name AzureDevopsUdacity

        ![image](./screenshot/workspace-azure-devops.png)

- Create Agent Pool
    - Create the VM as the Agent Pool

        ![image](./screenshot/creating-node-pool-vm.png)
    - Created Completely Agent Pool

        ![image](./screenshot/created-vm-agent-pool.png)
    - Create Access Token Azure Devops

        ![image](./screenshot/create-access-token-azdevops.png)
    - Create the New Agent pools and Install via Script
        ```
        mkdir myagent && cd myagent
        tar zxvf vsts-agent-linux-x64-3.244.1.tar.gz
        ./config.sh
        ```

        ![image](./screenshot/config-azure-agent-pool.png)

        ```
        ./run.sh
        ```

        ![image](./screenshot/agent-pool-online.png)

- Create Azure Pipeline
    - Initial Azure Pipline 

        ![image](./screenshot/create-pipeline.png)

    - Verify the Azure Pipeline Work Well

        ![image](./screenshot/pipelines-work-well.png)
        ![image](./screenshot/agent-run-job-pipelines.png)

    - Create Service Connection

        ![image](./screenshot/create-service-connection.png)

## Running Azure App Service from Azure Pipelines automatic deployment
- Application Deployed via Pipeline Complete
    ![image](./screenshot/pipeline_deploy_app_complete.png)
    ![image](./screenshot/pipeline_deploy_app_complete-2.png)

## Successful prediction from deployed flask app in Azure Cloud Shell. 
- [Use this file as a template for the deployed prediction](https://github.com/udacity/nd082-Azure-Cloud-DevOps-Starter-Code/blob/master/C2-AgileDevelopmentwithAzure/project/starter_files/flask-sklearn/make_predict_azure_app.sh).
- The screenshot of this output
    ![image](./screenshot/make_predict_azure_app_cloudshell.png)


```bash
odl_user [ ~/udacity-azure-devops ]$ ./make_predict_azure_app.sh 
Port: 443
{"prediction":[2.431574790057212]}
odl_user [ ~/udacity-azure-devops ]$ 
```

## Enhancements

To improve your deployment process, I recommend that we create a dedicated branch and a separate testing environment. This allows you to isolate new features and fixes from the main codebase, enabling thorough testing without impacting production. Set up CI/CD practices to automate testing and deployment, ensuring a smoother and more reliable release process.

* Output of streamed log files from deployed application
./webapp_log.zip file 

> 

## Demo 

https://youtu.be/fTzgorgyxpY


- Github Action Test Run Successfully

    ![image](./screenshot/github_action_test_run.png)