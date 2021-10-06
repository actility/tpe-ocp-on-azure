# tpeOcpAzure
ARM template to deploy TPE OCP on Azure

Prerequisites - AZ CLI - https://docs.microsoft.com/en-us/cli/azure/install-azure-cli

Run the following command:
```
az group deployment create --name tpeDeploy --resource-group <your-resource-group> --template-file Actility-Tpe-XS-Deploy.json
```

Once finalized, an Azure Image will be made available to all and id will be part of the template