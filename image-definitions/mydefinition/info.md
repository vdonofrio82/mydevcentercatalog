

# Dev Box Image Customization Guide

---

## Prerequisites

Before proceeding, ensure the following requirements are met:

- **Microsoft Dev Box service enabled** in your Azure subscription.
- **Dev Center and Project Catalogs configured** in your environment.
- **Sufficient permissions**: You must have the permissions, to create and manage image definitions and customizations.
- **Azure CLI installed** ([Install guide](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli)).
- **Dev Center extension for Azure CLI installed** (see below).
- **Network access**: Your environment must allow outbound connections to required Azure endpoints. For details, see [Dev Box networking requirements](https://learn.microsoft.com/en-us/azure/dev-box/networking).
- **Access to the Azure portal** ([portal link](https://portal.azure.com/)) for management tasks, if needed.
- **Windows 11 Enterprise multi-session or Windows 11 Enterprise base images** are recommended for most scenarios.

---

## Getting Started

Install the Dev Center extension for Azure CLI, run:

```bash
az extension add --name devcenter
```

Get a list of images to which your Dev Center has access, run:

```bash
az devcenter admin image list --dev-center-name ade-demo-devcenter --resource-group ade-demo-rg --query "[].{Name:name,Description:description}" --output table
```

The output will contain the name of the image to put in the `image` field of the definition file.

---


## Test the Image Definition

You can test your image definition by provisioning a Dev Box and verifying that your customizations are applied as expected. One convenient way to do this is by using the [Visual Studio Code Dev Box extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.dev-box).

### Steps to Test with VS Code Dev Box Extension

1. **Connect to your Dev Box:**
   - Once provisioning is complete, connect to the Dev Box directly from VS Code.
   - You can open a remote session, browse files, and use the integrated terminal

2. **Install or access VS Code and clone the repository:**
   - Access VS Code and clone the repository containing this image definition files.
   - Update the imagedefinition file with your customizations and configurations (like the base image name)

3. **Install the Dev Box extension for VS Code:**
   - Open the Extensions view in VS Code (`Ctrl+Shift+X`).
   - Search for "Dev Box" and install the official extension by Microsoft.

4. **Sign in to your Azure account:**
   - Use the command palette (`Ctrl+Shift+P`) and run `Azure: Sign In` if you are not already signed in.

5. **Open the Dev Box extension panel:**
   - Click on the Dev Box icon in the Activity Bar or search for "Dev Box" in the command palette.
   - Execute the command `Dev Box: Apply Customizations Tasks` to test the image definition.

6. **Verify your customizations:**
   - Check that all system and user tasks defined in your image definition have been applied correctly (e.g., installed software, configured settings).

For more details, see the [Dev Box extension documentation](https://learn.microsoft.com/en-us/azure/dev-box/vscode-extension).

## Understanding System Tasks vs User Tasks

**System tasks:** These tasks are located under the `tasks` section and run as LocalSystem during the provisioning stage of the dev box. They're typically used for system-level configurations, such as installing software or configuring system settings that require administrative privileges.

**User tasks:** These tasks are located under the `userTasks` section and run as the user **after the user's first sign-in to the dev box**. They're typically used for user-level configurations, such as installing user-specific applications or configuring user settings under user context. For example, users often prefer to install Python and Visual Studio Code under user context instead of systemwide. Put WinGet tasks in the userTasks section for better results when they don't work under tasks.

## References and Further Reading

- [Dev Box documentation overview](https://learn.microsoft.com/en-us/azure/dev-box/)
- [Reference: Dev Box customizations](https://learn.microsoft.com/en-us/azure/dev-box/reference-dev-box-customizations)
- [How to create and manage image definitions](https://learn.microsoft.com/en-us/azure/dev-box/how-to-create-manage-image-definitions)
- [How to customize Dev Box images](https://learn.microsoft.com/en-us/azure/dev-box/how-to-customize-dev-box)
- [Dev Box FAQ](https://learn.microsoft.com/en-us/azure/dev-box/dev-box-faq)

