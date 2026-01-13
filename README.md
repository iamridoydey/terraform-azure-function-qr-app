# Azure Function App with Terraform Deployment

## 📌 Overview
This project demonstrates how to provision an **Azure Function App** using **Terraform** and then deploy the function code locally using the **Azure Functions Core Tools (func CLI)**.  
It combines Infrastructure-as-Code (IaC) with a simple deployment workflow, ensuring reproducibility and maintainability.

---

## 🏗️ Architecture
- **Terraform** provisions:
  - Resource Group
  - Storage Account (for Function state and triggers)
  - App Service Plan
  - Function App

- **Azure Functions Core Tools (func CLI)** handles:
  - Local build and packaging
  - Deployment of function code to the provisioned Function App

---

## ⚙️ Prerequisites
Before you begin, ensure you have the following installed:

- [Terraform](https://developer.hashicorp.com/terraform/downloads) (v1.x+)
- [Azure CLI](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli) (latest)
- [Azure Functions Core Tools](https://learn.microsoft.com/en-us/azure/azure-functions/functions-run-local) (v4+)
- [Node.js](https://nodejs.org/) or other runtime supported by Azure Functions (depending on your function language)
- An active [Azure subscription](https://azure.microsoft.com/)

---

## 🚀 Setup & Deployment

### 1. Clone the Repository
```bash
git clone https://github.com/your-username/azure-function-terraform.git
cd azure-function-terraform
```

### 2. Get important env variables
```bash
az login

az ad sp create-for-rbac -n az-demo --role="Contributor" --scopes="/subscriptions/$AZURE_SUBSCRIPTION_ID"
```

### 3. Fill the data in placeholder and run it in terminal
```bash
export ARM_CLIENT_ID="${CLIENT_ID}"
export ARM_CLIENT_SECRET="${CLIENT_SECRET}"
export ARM_SUBSCRIPTION_ID="${SUBSCRIPTION_ID}"
export ARM_TENANT_ID="${TENANT_ID}"
```
### 4. Change the directory
```bash
cd azure-qr-code/qrCodeGenerator/
```
### 5. Install Dependencies

```bash
npm install
```

### 6. Local Configuration

Set up your `local.settings.json` file with the necessary configuration values:

```json
{
    "IsEncrypted": false,
    "Values": {
        "AzureWebJobsStorage": "<YOUR_STORAGE_CONNECTION_STRING>",
        "FUNCTIONS_WORKER_RUNTIME": "node",
	      "STORAGE_CONNECTION_STRING":"<YOUR_STORAGE_CONNECTION_STRING>"
    }
}
```

### 6. Running Locally

To start the function app locally, make sure you have Azure Functions Core Tools installed, then run:

```bash
func start
```

### 7. Deploy to Azure

Deploy your function app to Azure using the following command:

```bash
func azure functionapp publish <YOUR_FUNCTION_APP_NAME> --publish-local-settings 

func azure functionapp publish <YOUR_FUNCTION_APP_NAME>
```


### 8. Open browser / postman

```bash
https://<YOUR_FUNCTION_APP_NAME>.azurewebsites.net/api/GenerateQRCode?url=https://example.com
```