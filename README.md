Automation of Azure DevOps Pipelines via Logic App
This repository is designed to demonstrate a practical implementation of automating Azure DevOps Pipelines using a Logic App, following the guidelines set by the architecture example provided by Azure. It includes an ARM template for setting up a Logic App which serves as a mediator to streamline the creation and management of Azure DevOps Multi Stage Pipelines.

Within this source code, you'll find:

LogicApp.json: The ARM template for initializing the Logic App.
LogicApp.parameters.json: A parameters file that provides inputs to the ARM template for the Logic App setup.
Please ensure to customize the parameter values to fit your Azure DevOps organization, including your project details and Personal Access Token (PAT).

Note: After the development phase, it's crucial to secure your ARM template secrets, ideally by storing them in Azure Key Vault as securestring.

Pre-requisites for Deployment
To effectively deploy and utilize this project, ensure you have:

An Azure Subscription with available credits.
An Azure DevOps Account with administrative access to a project.
A current Azure DevOps Project in use.
A Personal Access Token (PAT) from Azure DevOps, which can be generated as described here.
The latest version of Visual Studio, preferably 2022 or newer.
Steps for Deploying Azure Resources
The deployment can be performed either via Visual Studio or Azure Cloud Shell. The process for deploying through Visual Studio can be found here.

Alternatively, deployment scripts can be executed in Azure Cloud Shell after cloning this repository, navigating to the specific project directory, and ensuring the template and parameter files are available in your Cloud Shell environment.

Deploy using the following Azure CLI commands:

shell
Copy code
az group create --name azdevops-multistage-pipelines --location "West Europe"
az deployment group create --resource-group azdevops-multistage-pipelines --template-file LogicApp.json --parameters LogicApp.parameters.json
For additional information on parameter file usage for ARM templates, refer to this Microsoft guide.

Integrating Logic App with Azure DevOps as a Service Hook
After the Logic App deployment:

Record the trigger URL from the provisioned Logic App.
Access the Project Settings in Azure DevOps and navigate to service hooks.
Set up a webhook for the Code Pushed event to link to the HTTP Trigger URL of the Logic App.
Subsequently, any code push within the specified Azure DevOps project will activate the Logic App, which then utilizes Azure DevOps APIs to set up the Multi Stage Pipelines as defined by the YAML file in the root of each repository.

This setup fosters a consistent and automated deployment mechanism throughout your Azure DevOps project repositories.
