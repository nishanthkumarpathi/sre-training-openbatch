# Azure Terraform Setup

### Prerequisites

* An Azure subscription. If you do not have an Azure account, [create one now](https://azure.microsoft.com/en-us/free/). This tutorial can be completed using only the services included in an Azure [free account](https://azure.microsoft.com/en-us/free/free-account-faq/).

If you are using a paid subscription, you may be charged for the resources needed to complete the tutorial.

* Terraform 0.14.9 or later
* The Azure CLI Tool installed

### Install the Azure CLI tool

You will use the Azure CLI tool to authenticate with Azure.

Follow the below link to install Azure CLI

{% embed url="https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-windows?tabs=azure-cli" %}

### Authenticate using the Azure CLI

Terraform must authenticate to Azure to create infrastructure.

In your terminal, use the Azure CLI tool to setup your account permissions locally.

```shell-session
az login
```

Your browser will open and prompt you to enter your Azure login credentials. After successful authentication, your terminal will display your subscription information.

You have logged in. Now let us find all the subscriptions to which you have access...

![](<../.gitbook/assets/image (2).png>)



Find the `id` column for the subscription account you want to use.

Once you have chosen the account subscription ID, set the account with the Azure CLI.

```shell-session
az account set --subscription "35akss-subscription-id"
```

### Create a Service Principal

Next, create a Service Principal. A Service Principal is an application within Azure Active Directory with the authentication tokens Terraform needs to perform actions on your behalf. Update the `<SUBSCRIPTION_ID>` with the subscription ID you specified in the previous step.

```
az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/<SUBSCRIPTION_ID>"
```

### Set your environment variables <a href="#set-your-environment-variables" id="set-your-environment-variables"></a>

HashiCorp recommends setting these values as environment variables rather than saving them in your Terraform configuration.

In your Powershell terminal, set the following environment variables. Be sure to update the variable values with the values Azure returned in the previous command.

```powershell
$Env:ARM_CLIENT_ID = "<APPID_VALUE>"
$Env:ARM_CLIENT_SECRET = "<PASSWORD_VALUE>"
$Env:ARM_SUBSCRIPTION_ID = "<SUBSCRIPTION_ID>"
$Env:ARM_TENANT_ID = "<TENANT_VALUE>"
```

### Write configuration

Create a folder called `terraform-azure`

```json5
# Configure the Azure provider
terraform {
  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "~> 3.0.2"
    }
  }

  required_version = ">= 1.1.0"
}

provider "azurerm" {
  features {}
}

resource "azurerm_resource_group" "rg" {
  name     = "myTFResourceGroup"
  location = "westus2"
}
```

### Initialize your Terraform configuration

Initialize your `terraform-azure` directory in your terminal. The `terraform` commands will work with any operating system. Your output should look similar to the one below.

```
terraform init
```

### Format and validate the configuration

We recommend using consistent formatting in all of your configuration files. The `terraform fmt` command automatically updates configurations in the current directory for readability and consistency.

Format your configuration. Terraform will print out the names of the files it modified, if any. In this case, your configuration file was already formatted correctly, so Terraform won't return any file names.

```shell-session
terraform fmt
```

You can also make sure your configuration is syntactically valid and internally consistent by using the `terraform validate` command.

Validate your configuration. The example configuration provided above is valid, so Terraform will return a success message.

```shell-session
terraform validate
```

### Apply your Terraform Configuration

Run the `terraform apply` command to apply your configuration.

This output shows the execution plan and will prompt you for approval before proceeding. If anything in the plan seems incorrect or dangerous, it is safe to abort here with no changes made to your infrastructure. Type `yes` at the confirmation prompt to proceed.

```
terraform apply
```

### Inspect your state

When you apply your configuration, Terraform writes data into a file called `terraform.tfstate`. This file contains the IDs and properties of the resources Terraform created so that it can manage or destroy those resources going forward. Your state file contains all of the data in your configuration and could also contain sensitive values in plaintext, so do not share it or check it in to source control.

Inspect the current state using `terraform show`.

```shell-session
terraform show
```

To review the information in your state file, use the `state` command. If you have a long state file, you can see a list of the resources you created with Terraform by using the `list` subcommand.

```shell-session
terraform state list
```
