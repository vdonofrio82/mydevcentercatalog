Pre-requisite for this example:
- MS DevBox implemented and Project catalogs configured
- Azure CLI installed and devcenter extension installed

To install the devcenter extension, run the following command:

```bash
az extension add --name devcenter
```
To get a list of images to which your dev center has access, run the following command:

```bash
az devcenter admin image list --dev-center-name ade-demo-devcenter --resource-group ade-demo-rg --query "[].{Name:name,Description:description}" --output table
```

The output will contain the name of the image to put in the `image` field of the definition file.

You can find more info on the image customizations in the reference documentation:
https://learn.microsoft.com/en-us/azure/dev-box/reference-dev-box-customizations

