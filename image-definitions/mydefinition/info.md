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


System tasks: These tasks are located under the "tasks" section and run as LocalSystem during the provisioning stage of the dev box. They're typically used for system-level configurations, such as installing software or configuring system settings that require administrative privileges.
User tasks: These tasks are located under the "userTasks" section and run as the user **after the user's first sign-in to the dev box**. They're typically used for user-level configurations, such as installing user-specific applications or configuring user settings under user context. For example, users often prefer to install Python and Visual Studio Code under user context instead of systemwide. Put WinGet tasks in the userTasks section for better results when they don't work under tasks.