# Exercise 1 - Create an Azure Spring Apps instance

In this section, we'll create an Azure Spring Apps instance using Azure CLI. While there are other ways of creating Azure resources, Azure CLI is the quickest and simplest method.

---
### Task 1: Verify Azure Subscription

1. Minimize the Azure portal and search for **git** in the Search Box then select **Git Bash**.

   ![Git bash](../01-create-an-azure-spring-cloud-instance/media/git-bash.png)
   
2. In **Git Bash** run the below commands. Make sure you enter these commands and all others that follow in **Git Bash**. **Do not use WSL, CloudShell, or any other shell.**, Ensure your Azure CLI is logged into your Azure subscription.           
           
   ```
   az login # Sign into an azure account
   ```
 
   > **Note:** Once you run the command, you will be redirected to the default browser, and then enter the **AD username:** <inject key="AzureAdUserEmail"></inject> and **Password:** <inject key="AzureAdUserPassword"></inject>, close the tab when you see the successful login message and proceed with the next command.

    ```
    az account show # See the currently signed-in account.
    ```

### Task 2: Create an Azure Spring Apps instance

1. In this section, we will create our Azure Spring Apps instance using Azure CLI.

2. First, you will need to come up with a name for your Azure Spring Apps instance.

3. The name must be unique among all Azure Spring Apps instances across all of Azure. Consider using **azure-spring-apps-lab-<inject key="DeploymentID" enableCopy="false" />** as a name for your Azure Spring Apps instance.

4. To limit typing, set the variable `AZ_RESOURCE_GROUP` to the name of the resource group **spring-apps-workshop-<inject key="DeploymentID" enableCopy="false"/>**. And set the variable `AZ_SPRING_CLOUD_NAME` to **azure-spring-apps-lab-<inject key="Deployment ID" enableCopy="false"/>**

   * Make sure to substitute the DID with **<inject key="DeploymentID" enableCopy="True"/>** in `AZ_RESOURCE_GROUP` and `AZ_SPRING_CLOUD_NAME`. Run the below mentioned command in **Git Bash**.

    ```bash
    AZ_RESOURCE_GROUP=spring-apps-workshop-DID
    AZ_SPRING_APPS_NAME=azure-spring-apps-lab-DID
    az config set extension.use_dynamic_install=yes_without_prompt
    ```

5. With these variables set, we can now create the Azure Spring Apps instance by running the below commands. To enable the Java in-process monitoring agent, we add the `enable-java-agent` flag.

    ```bash
    az spring create \
    -g "$AZ_RESOURCE_GROUP" \
    -n "$AZ_SPRING_APPS_NAME" \
    --enable-java-agent \
    --sku standard
    ```

6. For the remainder of this workshop, we will be running Azure CLI commands referencing the same resource group and Azure Spring Apps instance. So let's set them as defaults, so we don't have to specify them again.

   ```
   az configure --defaults group=$AZ_RESOURCE_GROUP
   az configure --defaults spring=$AZ_SPRING_APPS_NAME
   ```

---
