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

<TODO:  
* Architectural Diagram (Shows how key parts of the system work)>

<TODO:  Instructions for running the Python project.  How could a user with no context run this project without asking you for any help.  Include screenshots with explicit steps to create that work. Be sure to at least include the following screenshots:

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
    az webapp up --name flask-ml-toanla --resource-group Azuredevops --runtime "PYTHON:3.8" --sku FREE
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

* Successful deploy of the project in Azure Pipelines.  [Note the official documentation should be referred to and double checked as you setup CI/CD](https://docs.microsoft.com/en-us/azure/devops/pipelines/ecosystems/python-webapp?view=azure-devops).

* Running Azure App Service from Azure Pipelines automatic deployment

* Successful prediction from deployed flask app in Azure Cloud Shell.  [Use this file as a template for the deployed prediction](https://github.com/udacity/nd082-Azure-Cloud-DevOps-Starter-Code/blob/master/C2-AgileDevelopmentwithAzure/project/starter_files/flask-sklearn/make_predict_azure_app.sh).
The output should look similar to this:

```bash
udacity@Azure:~$ ./make_predict_azure_app.sh
Port: 443
{"prediction":[20.35373177134412]}
```

* Output of streamed log files from deployed application

> 

## Enhancements

<TODO: A short description of how to improve the project in the future>

## Demo 

<TODO: Add link Screencast on YouTube>