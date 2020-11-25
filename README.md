# Azure Managed Application - Hello World Example (September 2020)

This repo contains a simple "Hello World" style example of Azure Managed application that is used in this video tutorial [Simple Azure Managed Application: creating, testing, and publishing in Partner Center](https://medium.com/@ArsenVlad/simple-azure-managed-application-creating-testing-and-publishing-in-partner-center-d2cb3b98bed2)

> Important: When building your Azure Application ARM templates for submission to Azure Marketplace, please make sure to carefully follow all of the guidelines and practices described [here](https://github.com/Azure/azure-quickstart-templates/blob/master/1-CONTRIBUTION-GUIDE/best-practices.md) and be ready to make fixes and changes based on [manual review feedback](https://docs.microsoft.com/en-us/azure/marketplace/partner-center-portal/azure-apps-review-feedback).

Test the application using <http://github.com/Azure/arm-ttk> tool

```cmd
C:\Code\GitHub\Azure\arm-ttk\arm-ttk\Test-AzTemplate.cmd
```

Zip and AzCopy to storage

```bash
tar -a -c -f ama.zip createUiDefinition.json mainTemplate.json viewDefinition.json

azcopy copy ./ama-aks.zip "https://YOUR_STORAGE_ACCOUNT.blob.core.windows.net/YOUR_STORAGE_CONTAINER/ama-aks.zip?SHARED_ACCESS_SIGNATURE_WITH_WRITE_PERMISSION"
```

Create managed application definition

```bash
az group create --name avama --location eastus

az managedapp definition create --name "ama-definition" --location eastus --resource-group avama --lock-level ReadOnly --display-name "Hello World App Definition" --description "Azure Managed App Hello World Example" --authorizations "YOUR_AAD_GROUP_PRINCIPAL_ID:b24988ac-6180-42a0-ab88-20f7382dd24c" --package-file-uri "https://YOUR_STORAGE_ACCOUNT.blob.core.windows.net/ama-aks/ama-aks.zip"
```
