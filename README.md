# ThingPark Enterprise deployment on Microsoft Azure

Easily deploy ThingPark Enterprise (TPE) with [Azure Resource Manager (ARM) template](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/overview).

## Project structure

- Actility-TPE-\<segment\>-Deploy.json: Azure Resource Management (ARM) templates.

For more details about the hardware sizing **segments**, please refer to the [ThingPark Enterprise documentation]([https://thingpark.page.link/TPE-OCP_sizing](https://docs.thingpark.com/thingpark-enterprise/7.3/docs/ocp-tpe/appliance/size-hardware)

## Prerequisites

- Azure account
- Azure command line interface (CLI) (https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
- Actility shared compute gallery informations, [contact us](mailto:operations-enterprise@actility.com):
  - Application (client) ID
  - Secret value
  - Actility tenant ID

## Getting started

### Request access to application

The ThingPark Enterprise ARM template will deploy an Azure Image available in a shared Azure Compute Gallery.

Replace _\<your Tenant ID>_ with the tenant ID who wants to use the image gallery. Replace _\<Application (client) ID>_ with the application ID provided by Actility.
When done making the replacements, paste the URL into a browser and follow the sign-in prompts to sign into your account.

```text
https://login.microsoftonline.com/<your Tenant ID>/oauth2/authorize?client_id=<Application (client) ID>&response_type=code&redirect_uri=https%3A%2F%2Fwww.microsoft.com%2F 
```

### Create a contributor role for the application in the resource group where you will deploy Thingpark Enterprise

1. Select the resource group and then select Access control (IAM). Under Add role assignment select Add.
2. Under Role, type Contributor.
3. Under Assign access to:, leave this as Azure AD user, group, or service principal.
4. Under Select type _actility_operation_gallery_ then select it when it shows up in the list. When you are done, select Save.

### Create a scale set using Azure CLI

Sign in the service principal for Actility tenant using the application ID, Secret and the Actility tenant ID:

```shell
az account clear
az login --service-principal -u '<Application (client) ID>' -p '<Secret>' --tenant '<Actility tenant ID>'
az account get-access-token
```

Sign in the service principal for your tenant using the application ID, Secret and your tenant ID:

```shell
az login --service-principal -u '<Application (client) ID>' -p '<Secret>' --tenant '<your tenant ID>'
az account get-access-token
```

### Deployment

```shell
az deployment group create --name tpeDeploy --resource-group <your-resource-group> --template-file Actility-Tpe-XS-Deploy.json --aux-tenants <Actility tenant ID>
```
