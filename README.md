# tpeOcpAzure
ARM template to deploy TPE OCP on Azure using Actility shared image.

Prerequisites - AZ CLI - https://docs.microsoft.com/en-us/cli/azure/install-azure-cli

Get from Actility - App information of shared gallery where TPE image is stored.
    - Application name
    - Actility tenant ID
    - App (client) ID
    - secret
    
Request access to application by signing in to the following link

```
https://login.microsoftonline.com/<your Tenant ID>/oauth2/authorize?client_id=<Application (client) ID>&response_type=code&redirect_uri=https%3A%2F%2Fwww.microsoft.com%2F 
```

Create a contributor role for the application in the resource group where you will deploy TPE

    1- Select the resource group and then select Access control (IAM). Under Add role assignment select Add.
    2- Under Role, type Contributor.
    3- Under Assign access to:, leave this as Azure AD user, group, or service principal.
    4- Under Select type myGalleryApp then select it when it shows up in the list. When you are done, select Save.

Create a scale set using Azure CLI

Actility tenant:
```
az account clear
az login --service-principal -u '<app ID>' -p '<Secret>' --tenant '<Actility tenant ID>'
az account get-access-token
```

Using your tenant ID:
```
az account clear
az login --service-principal -u '<app ID>' -p '<Secret>' --tenant '<your tenant ID>'
az account get-access-token
```


You can now deploy TPE using ARM:
```
az deployment group create --name tpeDeploy --resource-group <your-resource-group> --template-file Actility-Tpe-XS-Deploy.json --aux-tenants <Actility tenant ID>
```
