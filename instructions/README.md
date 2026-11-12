# Attendee instructions


## Welcome to Your Lab Environment - End to end Resiliency

For in-person lab attendees, sign in to the provided Windows 11 virtual machine using the username and password supplied by your lab provider. If you are following these instructions outside the hosted lab, use your own workstation; no lab virtual machine sign-in is required.

# Hands-on with Resiliency in Azure: Assess, Recommend, Recover

## Story Overview

Caldova is launching **CaldovaPayApp** to support its expansion into a new market. With customer transactions expected to surge during the holiday season, Caldova must build resiliency into the application from day one rather than retrofit it later. The growing transaction volume also makes Caldova a more attractive target for cyber threats. You are the Platform Architect for Caldova and you will take key decisions to ensure Caldova is prepared for the upcoming challenge.


## What you will do

Simulate the journey of Caldova, a financial services firm, launching its payments application, **CaldovaPayApp**, on Azure with a focus on:

- Infrastructure Resiliency
- Data Resiliency
- Cyber Recovery

By the end of this lab, Caldova will:

- 🏗️ Have deployed CaldovaPayApp from an IaC template with zonal resiliency built in from the start.
- ✅ Have its cloud-native workloads backed up in a vault hardened against ransomware.
- 🛡️ Be able to identify compromised recovery points and recover virtual machines in bulk from verified clean snapshots.
- 🌐 Have its application resources grouped and assessed against zonal resiliency goals.
- 🔁 Have a recovery plan in place to orchestrate recovery.


> [!TIP]
> In the hosted lab, find your virtual machine credentials, Azure sign-in credentials and assigned subscription on the **Resources** tab beside **Instructions**. Outside the hosted lab, use your own Azure account and the subscription containing the exercise resources. To find its subscription ID, open **Subscriptions** in the Azure portal, select that subscription and copy **Subscription ID** from **Overview**.


===

### 🛠️ Task 1: Generate a Resilient IaC Template with the Resiliency Agent

1. Sign in to the [https://aka.ms/AzureResiliency/regionalpreview](https://aka.ms/AzureResiliency/regionalpreview) using your assigned lab Azure credentials, or your own Azure account outside the hosted lab.
    1. Use the Azure portal from the above link for the entire duration of the lab as we are going to present to you some of the features that are still in preview that are available with the above link
2. Open **Azure Copilot** from the top bar of the portal and select **Resiliency** from the **New chat** options.
    - You can also open the agent from the top actions on the **Resiliency** overview page.
3. Review the CaldovaPayApp architecture below. A copy, **CaldovaPayApp Architecture**, is also available in the D drive. You can locate it using Windows Explorer. 

<img src="[[https://github.com/Charmila1.png](https://github.com/microsoft/ignite26-LAB721/blob/main/docs/CaldovaPayAppArchitectureV2Download.png)](https://github.com/microsoft/ignite26-LAB721/blob/main/docs/CaldovaPayAppArchitectureV2Download.png)" width="100px;" alt="CaldovaPayAppArchitectureV2Download"/>

4. Copy the prompt below into the agent chat and send it:

#### Options 1: Upload an architecture diagram

- You will find the architecture diagram in the D drive by the name **'CaldovaPayApp.png'** Attach that along with the prompt. 

```text
   I'm deploying a payments application called CaldovaPayApp into the resource group CaldovaPayApp_Ex3_Task1_DiscoveryAgent. Here is the Application  architecture diagram attached for the app. 
Generate a Bicep template that keeps this application running through an availability zone outage, and give me the commands to deploy it.
```


#### Option 2: Describe the application architecture to the agent

- Only use this if the architecture diagram upload is not working

    ```text
    I'm deploying a payments application called CaldovaPayApp into the resource group CaldovaPayApp_Ex3_Task1_DiscoveryAgent. It has:
    - Two web-tier virtual machines behind a public load balancer
    - Two application-tier virtual machines
    - An Azure Database for PostgreSQL flexible server for structured payments data
    - An Azure Storage account (Blob) for transaction documents and logs
    - One virtual network with separate subnets for the web, app and data tiers
    Tag every resource AppName = CaldovaPayApp. Generate a Bicep template that keeps this application running through an availability zone outage, and give me the commands to deploy it.
    ```

5. If the agent asks follow-up questions:
    - **Region:** use the region as **"EastUS"**
    - For anything else, accept the agent's recommendation.
    - Select 'Generate Bicep' when suggested by the agent
    - If asked for a subscription, use the assigned subscription on the **Resources** tab in the hosted lab, or the subscription containing your exercise resources outside the hosted lab.

    <!-- TODO (engineering): add the lab region capacity to the Skillable Resources tab. 
  Also to align with the narrative of  a new deployment, lets see if we should select a non US region where Caldova will venture.-->
6. Review the resiliency report. It shows how the agent analyzed your application topology and which resiliency configurations it recommends for each tier. Proceed with template generation.
7. Review the generated template. The agent produces modular files, including **main.bicep**, **parameters.json** and one file per resource.

  <!-- TODO (engineering): verify if this is the correct generated artifacts' list. Else update. -->

💡 Note: The Resiliency agent doesn't make changes to your resources. All actions require your confirmation and manual execution.

✅ By the end of this task, you have a deployment-ready Bicep template for CaldovaPayApp with resiliency configurations already enabled.


===

### 🛠️ Task 2: Deploy the Template (This is to be tested an updated. Read it as a placeholder. Mainly generated by AI)

The Resiliency agent gives you the commands to deploy your template. You run them in Azure Cloud Shell.

1. Open **Cloud Shell** from the top bar of the Azure portal.
2. Select the **PowerShell** option.
3. Choose **No storage account required**.
4. Select your subscription and click **Apply**.
5. Once Cloud Shell is ready, run the deployment commands from the agent's response:
    - Make sure the target resource group is **CaldovaPayApp_Ex3_Task1_DiscoveryAgent**.
    - If prompted for a virtual machine admin password, enter a password of your choice that meets Azure's complexity requirements.

    <!-- TODO (engineering): confirm how the generated template files reach Cloud Shell (download and upload, or commands that include the template) and add the exact steps here. -->
6. Confirm the deployment has started. Leave it running and continue to Task 3. Deployment takes several minutes.

> [!IMPORTANT]
> If the template fails validation or the deployment fails, don't troubleshoot it. There isn't time in this exercise. Continue to Task 3. A pre-deployed copy of the same application is ready for you to use in Exercise 3.

✅ By the end of this task, CaldovaPayApp is deploying into **CaldovaPayApp_Ex3_Task1_DiscoveryAgent** with zonal resiliency built in. The expansion of the business in the new Region will be resilient to zonal outages.

> [!knowledge] Resiliency agent is also now available from Github Copilot in VSCode to help you generate and validate your deployment templates for resiliency!!


  <!-- TODO (engineering): provide the exact name which we ive to the user. If not possible, lets change this end sentence to something generic. -->

===

### 🛠️ Task 3: Review the Converged Resiliency View for Your Estate

While your deployment runs, look at the resiliency posture of Caldova's wider Azure estate.

1. Search for **Resiliency** in the portal search bar and open the Resiliency dashboard.
2. In the left menu, expand **Infrastructure Resiliency**. You will see **Overview**, **Resource Resiliency**, **Service Group Resiliency**, **Recommendations**, **Recovery Plans**, **Drills** and **Usage Plans**.
3. Select **Overview** to see the summary of zone resiliency posture across all your resources and service groups.
4. Select the **Resource resiliency** tile to see counts by resiliency status, then select through to the zone resiliency status of individual resources.
5. Select **Service group resiliency** to see posture at the application level for the service groups in your estate.

💡 Note: This view spans your whole estate, not just the app you are deploying. Resources from your in-progress deployment may not appear yet.

  <!-- TODO (Sagar): Check with Anam if this needs an explicit set of instructions beyond what is listed above.  -->

✅ By the end of this task, you have seen how an application's resiliency posture sits alongside the rest of Caldova's environment.

🔍 Example: Caldova's estate already includes copies of CaldovaPayApp that have been serving customers in other regions, each built with a different level of resiliency. Compare how their posture differs. We will address them in Exercise 3. Then look at the cloud-native workloads Caldova has deployed alongside them: do they have data protection configured witth Azure Backup?

✅ By the end of this task, you have seen how an application's resiliency posture sits alongside the rest of Caldova's environment.

### ➡️ Up Next: Protect Caldova's Data

===

### Exercise 2: Data Resiliency and Cyber Recovery with Azure Backup

## Contents

1. [Exercise 2: Data Resiliency and Cyber Recovery with Azure Backup](#exercise-2-data-resiliency-and-cyber-recovery-with-azure-backup)
    2. [Task 1: Create your Backup vault](#task-1-create-your-backup-vault)
    3. [Task 2: Enable backup on cloud-native workloads](#task-2-enable-backup-on-cloud-native-workloads)
        4. [2a. Protect Azure Data Lake Storage](#2a-protect-azure-data-lake-storage)
        5. [2b. Protect the AKS cluster](#2b-protect-the-aks-cluster)
        6. [2c. Protect Azure Cosmos DB](#2c-protect-azure-cosmos-db)
    7. [Task 3: Review threat detection signals](#task-3-review-threat-detection-signals)
    8. [Task 4: Perform a bulk restore of virtual machines](#task-4-perform-a-bulk-restore-of-virtual-machines)
    9. [Lab environment reference](#lab-environment-reference)

Select a link above, or choose **Next** to begin.

===
# Exercise 2: Data Resiliency and Cyber Recovery with Azure Backup

### 🎯 Goal

Protect CaldovaPayApp's cloud-native data with Azure Backup, then use threat signals to pick a clean recovery point and recover virtual machines at scale.

### 🏢 Caldova's Approach

Caldova's expansion has meant shipping fast. New cloud-native workloads went live in every region, and nobody stopped to configure backup. Zone resiliency keeps CaldovaPayApp running through an outage, but it won't protect Caldova's data from an attacker.

Last holiday season, Caldova was hit by an unprecedented wave of ransomware attacks, and the ransom demands that followed were costly. With transactions about to surge again, Caldova expects the attackers back.

In this exercise, you'll put Caldova's cloud-native data under Azure Backup protection. Then you'll face an attack head-on: Microsoft Defender for Cloud detects a threat on Caldova's servers, and you'll restore them in bulk from recovery points verified as clean, with no ransom paid.

===
## Task 1: Create your Backup vault

Azure Backup uses two vault types, and the workload decides which one you need.

| Vault type | Used in this exercise for |
| --- | --- |
| **Backup vault** | Azure Data Lake Storage, AKS, Azure Cosmos DB - **one vault protects all three** |
| **Recovery Services vault** | Azure Virtual Machines - already provisioned for you as **rsv-&lt;unique-suffix&gt;-1**, used in Tasks 3 and 4 |

In this task you create a **Backup vault**.

---

> [!Note] 🛟 You can create the Backup Vault using either Resiliency Agent (Option A) or the Azure portal (Option B), based on your preference.

### Option A - Create the vault using the Resiliency agent

<!-- TODO (Charmila): test this option end to end in the lab environment. -->

1. Check the region where Resource Group **Exercise2_UnProtectedWorkloadsSet1**  is created by searching for Resource Groups.
2. Open **Azure Copilot** from the top bar of the portal and select **Resiliency**, as you did in Exercise 1.
3. Copy the prompt below into the agent chat, edit the region as per the RG region and aubmit it:

   ```text
   Create a Backup vault named CaldovaPay-Agent-BackupVault in resource group Exercise2_UnProtectedWorkloadsSet1 in the <Region> region, using geo-redundant storage. Do not enable immutability.
   ```

3. Before you accept, confirm the agent's proposal shows:
   - **Vault type**: **Backup vault**
   - **Name**, **resource group** and **region** as in the prompt
   - **Immutability**: not enabled
4. Select the confirmation action the agent presents to submit the deployment.
   <!-- TODO (Charmila): replace with the exact button name once tested. -->
5. When the deployment succeeds, confirm the vault is listed under **Resiliency → Backup and recovery → Vaults**.

---

### Option B - Create the vault from the Azure portal

1. In the portal search bar, search for **Resiliency** and open the **Resiliency** dashboard.
2. In the left navigation, expand **Backup and recovery** and select **Vaults**.
3. Select **+ Vault**.

4. For vault type, choose **Backup vault**, then select **Continue**.
5. On the **Basics** tab, enter:
   - **Subscription**: your lab subscription
   - **Resource group**: `Exercise2_UnProtectedWorkloadsSet1`
   - **Backup vault name**: `CaldovaPay-Agent-BackupVault`
   - **Region**: **Australia Central**
   - **Backup storage redundancy**: **Geo-redundant**

6. Select **Review + create**, then **Create**.

> [!Note] 🛟 If vault creation fails, or the deployment is still running after **2 minutes**, don't wait: continue to Task 2, which uses the pre-created vault **backupvault-unprotected-&lt;unique-suffix&gt;-1**.

> ✅ **By the end of this task** you have created a Backup vault.

===

## Task 2: Enable backup on cloud-native workloads

CaldovaPayApp's data tier spans three services, and none of them are backed up: the transaction archive in **Azure Data Lake Storage**, the payments API on **AKS**, and the transaction ledger in **Azure Cosmos DB**. You'll protect all three with the same Backup vault, either use the vault you created in the previous task or use **backupvault-unprotected-&lt;unique-suffix&gt;-1**.

Each workload is configured the same way. Only the **Datasource type** you pick changes:

| Workload | Datasource type to select |
| --- | --- |
| Azure Data Lake Storage | **Azure Data Lake Storage** |
| AKS | **Azure Kubernetes services** |
| Azure Cosmos DB | **Azure Cosmos DB (Preview)** |

> [!Note] ⏱️ **Short on time?** The sections are independent. Configure 2a yourself, then review the pre-protected resources for 2b and 2c.

===
### 2a. Protect Azure Data Lake Storage

Azure Backup keeps a copy of Caldova's transaction archive in the vault, separate from the source storage account. [Learn more about vaulted backup for Azure Data Lake Storage](https://learn.microsoft.com/azure/backup/azure-data-lake-storage-backup-overview).

**Create the backup policy**

1. In the portal, open the Backup vault with **backupvault-unprotected-&lt;unique-suffix&gt;-1** (for example - backupvault-unprotected-66282771-1) and navigate to **Manage** -> **Backup policies**, then **+ Add**.
2. On the **Basics** tab, enter the **Policy name** `CaldovaPay-ADLS-Policy` and select **Datasource type** as **Azure Data Lake Storage**.
3. On the **Schedule + retention** tab, review the Backup Frequency and Retention settings for the default rule.
4. Click on Add retention rule -> Select Retention rule **Backup taken every month**, select **Vault-Standard** and click on **Add** and click on Next
5. Select **Review + create**, then **Create**.


**Configure protection**

1. Go to Backup vault **backupvault-unprotected-<unique-suffix>-1 → Overview** and select **+ Backup**.
2. On the **Basics** tab, select **Datasource type**: **Azure Data Lake Storage**, then select **Next**.
3. On the **Backup policy** tab, select **`CaldovaPay-ADLS-Policy`**, then select **Next**.
4. On the **Datasources** tab:
   - Select **Add**.
   - For **Storage account**, select **Add/Edit**.
   - Choose the storage account **adlsunprotected&lt;unique-suffix&gt;**.
   - Choose **Backup all present containers**.
   - Validation starts automatically. If it reports **Role assignment not done**, select the roles and choose **Assign missing roles**.
5. When validation shows **Success**, select **Configure Backup**.


> 🛟 Skip if the configuration is successful. If **Protection still can't be configured:** review the pre-protected storage account instead. Go to **Resiliency → Backup and recovery → Protected items**, set the **Datasource type** filter to **Azure Data Lake Storage**, and select **adlsprotected&lt;unique-suffix&gt;**.

> [!Note] ⏱️ The first recovery point takes time to appear. Don't wait for it; move on to 2b.

===
### 2b. Protect the AKS cluster

The Backup Extension is already installed on the cluster **aks-unprotected--&lt;unique-suffix&gt;-1**, so you can go straight to the policy. [Learn more about AKS backup](https://learn.microsoft.com/azure/backup/azure-kubernetes-service-backup-overview).


**Create the backup policy**

1. In the portal, open the Backup vault **backupvault-unprotected-&lt;unique-suffix&gt;-1** and select **Manage → Backup policies → + Add**.
2. Enter the **Policy name** `CaldovaPay-AKS-Policy` and select **Datasource type** as **Kubernetes Services**.
3. On the **Schedule + retention** tab, set **Backup Frequency** to **Daily** and keep the **Default** retention rule. 
4. Click on Add retention rule -> Select Retention rule **Backup taken every month**, select **Vault-Standard**, add **30** days retention duration and click on **Add**
5. Select **Next**, then select **Create** on the **Review + create** tab.

**Configure protection**

1. Go to **Backup vault backupvault-unprotected-&lt;unique-suffix&gt;-1 → Overview** and select **+ Backup**.
2. On the **Basics** tab, click on **Select Kubernetes cluster** under **Additional datasource scope** then select the resource **aks-unprotected--&lt;unique-suffix&gt;-1** and click **Select**.
   - If prompted to enable **Trusted Access** between the cluster and the vault or **Extension MSI Role Permissions are missing**, select **Grant Permission** and wait for it to complete.
3. On the **Backup policy** tab, select **`CaldovaPay-AKS-Policy`**, then select **Next**.
4. On the **Datasources** tab, select **Add/Edit**:
   - Enter **Backup Instance Name** `Caldova-AKS-Backup-Instance`
   - Under **Select Namespaces to backup**, choose **All**.
   - Leave **Additional Resource Settings** and **Backup Hooks** at their defaults, then select **Select**.
5. For **Snapshot resource group**, select `Exercise2_UnProtectedWorkloadsSet1`.
6. Select **Validate**. If validation reports missing roles, select the datasource checkbox and choose **Assign missing roles**.
7. When validation succeeds, select **Next**, then **Configure backup**.

>  🛟 Skip if the configuration is successful. If
 **Protection still can't be configured:** review the pre-protected cluster instead. Go to **Resiliency → Backup and recovery → Protected items**, set the **Datasource type** filter to **Azure Kubernetes services**, and select **aks-protected-&lt;unique-suffix&gt;-3**.

===
### 2c. Protect Azure Cosmos DB

Cosmos DB vaulted backup is in preview, and `caldovapay-cosmos` is already set up to support it. [Learn more about Azure Cosmos DB backup](https://learn.microsoft.com/azure/backup/backup-azure-cosmos-db-overview).

**Create the backup policy**

1. In the portal, open the Backup vault **backupvault-unprotected-&lt;unique-suffix&gt;-1** and select **Manage → Backup policies → + Add**.
2. Select **Datasource type** as **Azure Cosmos DB (Preview)**, then select **Continue**.
3. On the **Basics** tab, enter the **Policy name** `CaldovaPay-Cosmos-Policy`.
4. On the **Schedule + retention** tab, set **Backup Frequency** to **Daily** and keep the **Default** retention rule. 
5. On the **Review + create** tab, select **Create**.

**Configure protection**

1. Go to **Backup vault backupvault-unprotected-&lt;unique-suffix&gt;-1 → Overview** and select **+ Backup**.
2. On the **Basics** tab, select:
   - **Datasource type**: **Azure Cosmos DB (Preview)**
   - Then select **Next**.
3. On the **Backup policy** tab, select **`CaldovaPay-Cosmos-Policy`**, then select **Next**.
4. On the **Datasources** tab, select the datasource name, choose the Cosmos DB account **cosmos-unprotected-&lt;unique-suffix&gt;-1**, and select **Next**.
   - Validation runs automatically. If it reports **Role assignment not done or missing**, select **Assign missing roles**.
5. When validation shows **Success**, select **Next**, then select **Configure backup** on the **Review + configure** tab.




> **Azure Cosmos DB (Preview) isn't listed, or configuration couldn't be completed:** review the pre-protected account instead. Go to **Resiliency → Backup and recovery → Protected items**, set the **Datasource type** filter to **Azure Cosmos DB**, and select **cosmos-protected-&lt;unique-suffix&gt;-3**

> ✅ **By the end of this task** CaldovaPayApp's cloud-native data tier - the payments API platform and the transaction ledger - is protected by Azure Backup, all from a single Backup vault.

===
## Task 3: Review threat detection signals

Protection is in place, but which recovery point is safe to restore? Azure Backup uses signals from Microsoft Defender for Cloud to mark each virtual machine recovery point as clean or suspicious.

1. Go to **Resiliency → Backup and recovery** and select **Threat detection (Preview)** in the left navigation.
2. Review the summary tiles across the top, in particular **Resources with suspicious RPs**.
3. Review the **Scan status** and **Scan summary** columns across your protected items.

4. Select the protected item showing **Suspicious RPs found**.
5. Select through to the associated item and review its recovery points. Identify which show a **Recent scan status** of **Suspicious** and which show **No Threats Reported**.
6. Select a suspicious recovery point to view the scan details, including the Defender for Cloud alerts that caused it to be flagged.

> [!Hint] 💡 **Note the timestamp of the last clean recovery point** - the most recent one showing **No Threats Reported** before the suspicious ones begin. You'll restore from it in Task 4.

> [+Hint] Continue further if all recovery points are in "Healthy" state. Come back after completing all lab tasks to check if there are any "Suspicious" recovery points.

> ✅ **By the end of this task** you can tell a trustworthy recovery point from a compromised one, and you have identified the clean point to recover from.

===

## Task 4: Perform a bulk restore of virtual machines

A real ransomware attack rarely hits just one machine. **Bulk restore** recovers up to **100** virtual machines in a single guided flow, instead of running the restore wizard once per machine.

> [!NOTE]
> Bulk restore is in **preview**. It restores to an **alternate location**, so your original VMs are left untouched for investigation.

1. In the portal, search for Recovery Services vault and select the resource **rsv-&lt;unique-suffix&gt;-1**.
2. Go to **Protected items → Backup items**.
3. On the **Backup items** pane, select **Azure Virtual Machine** as the **BACKUP MANAGEMENT TYPE**.
4. Select **Bulk restore (Preview)** 
5. On the **Basics** tab, click on **Select** to select resources, select all the three VMs listed and click **Save**.
6. On the **Restore point** tab:
   - The latest restore point is selected by default for each VM.
   - For the VM you reviewed in Task 3, select **Edit** and choose the **last clean recovery point** you noted, the most recent one showing **No Threats Reported**.

   > [!IMPORTANT]
   > ⚠️ Restoring the newest recovery point would reintroduce the compromise. Always restore from the last point verified clean.

   - Select **Next**.
7. On the **Restore parameters** tab, set the restore target to **Create New** and set the following parameters:
   - **Restore Type**: **Create new virtual machine**
   - **Virtual machine name prefix**: `Caldova`
   - **Target resource group**: `Exercise2_VMs_Set1`
   - **Virtual Network**: Select **vnet-&lt;unique-suffix&gt;-1**
   - **Subnet**: **default**
   - **Staging Location**: Select **staging&lt;unique-suffix&gt;**
   - **Managed Identity**: `Disable`
   - Select **Next**.

8. On the **Validation pre-checks** tab, confirm all checks pass.
9. On the **Review + restore** tab, select **Restore** to start the bulk restore.
10. Track progress in the vault under **Monitoring** -> **Backup jobs**. Each VM restore runs as its own job.

> [!TIP]
> 💡 Restore time grows with the number and size of the VMs. You don't need to wait for the jobs to finish before moving on.

> ✅ **By the end of this task** CaldovaPayApp has recovered a fleet of virtual machines from a verified-clean recovery point in a single operation, into an isolated location where they can be validated before cutover.

===
## Summary

In this exercise you:

- Created a **Backup vault** using the **Resiliency agent**, with the portal as the alternative.
- Configured protection for **Azure Data Lake Storage**, an **AKS cluster** and an **Azure Cosmos DB** account, all from a single Backup vault.
- Used **Threat detection** signals from **Microsoft Defender for Cloud** to separate clean recovery points from suspicious ones.
- Performed a **bulk restore** of virtual machines from a verified-clean recovery point.

CaldovaPayApp's data tier is now protected, and its recovery decisions are driven by evidence rather than guesswork.

📋 Want to see everything that was set up for you in this exercise? See the [Lab environment reference](#lab-environment-reference).

---

### Learn more

- [Resiliency in Azure overview](https://learn.microsoft.com/azure/resiliency/resiliency-overview)
- [Azure Backup overview](https://learn.microsoft.com/azure/backup/backup-overview)
- [Create and manage Backup vaults](https://learn.microsoft.com/azure/resiliency/backup-vaults)
- [Create a Recovery Services vault](https://learn.microsoft.com/azure/backup/backup-create-recovery-services-vault)
- [Azure Data Lake Storage vaulted backup overview](https://learn.microsoft.com/azure/backup/azure-data-lake-storage-backup-overview)
- [Configure Azure Data Lake Storage backup](https://learn.microsoft.com/azure/backup/azure-data-lake-storage-configure-backup)
- [Azure Data Lake Storage backup support matrix](https://learn.microsoft.com/azure/backup/azure-data-lake-storage-backup-support-matrix)
- [Restore Azure Data Lake Storage](https://learn.microsoft.com/azure/backup/azure-data-lake-storage-restore)
- [AKS backup overview](https://learn.microsoft.com/azure/backup/azure-kubernetes-service-backup-overview)
- [Back up an AKS cluster](https://learn.microsoft.com/azure/backup/azure-kubernetes-service-cluster-backup)
- [AKS backup support matrix](https://learn.microsoft.com/azure/backup/azure-kubernetes-service-cluster-backup-support-matrix)
- [Azure Cosmos DB backup overview (preview)](https://learn.microsoft.com/azure/backup/backup-azure-cosmos-db-overview)
- [Configure Azure Cosmos DB backup (preview)](https://learn.microsoft.com/azure/backup/backup-azure-cosmos-db)
- [Threat detection in Azure Backup](https://learn.microsoft.com/azure/backup/threat-detection-overview)
- [Restore VMs with Azure Backup (including bulk restore)](https://learn.microsoft.com/azure/backup/backup-azure-arm-restore-vms)
- [Azure Copilot Resiliency Agent](https://learn.microsoft.com/azure/copilot/resiliency-agent)

===

# Hands-on with Resiliency in Azure: Assess, Recommend, Recover

## Exercise 3: Get Resilient - Assess CaldovaPayApp

## 🎯 Goal

Learn how to discover the Azure resources that make up an application, group them together, assign a resiliency goal, and assess the application for resiliency gaps.

## 🏢 Caldova's Approach

In Exercise 1, you saw how the Resiliency agent can build zonal resiliency into CaldovaPayApp from the start. You also reviewed Caldova's broader Azure estate and saw different versions of CaldovaPayApp with different resiliency postures.

Now, you will zoom in on one application.

Caldova needs a single application-level view of all the resources that support CaldovaPayApp. The platform team will use the Resiliency agent to discover the application, group its resources into a Service Group, assign a zonal and regional resiliency goal, and assess the application for remaining gaps.

In this exercise, you will:

1. Discover the resources that make up CaldovaPayApp.
2. Group those resources into a Service Group.
3. Assign a zonal and regional resiliency goal.
4. Assess the application's resiliency posture.
5. Review recommendations for any remaining gaps.

===

## Application Used in This Exercise

Use the pre-deployed application in the Resource group:

**CaldovaPayApp_Ex3_Task1**

This pre-deployed application represents a non resilient version of the CaldovaPayApp architecture that you worked with in Exercise 1. It provides a consistent environment regardless of whether the deployment started in Exercise 1 has completed.

===

# 🛠️ Task 1: Discover CaldovaPayApp

In Exercise 1, you reviewed the resiliency posture of Caldova's entire Azure estate. In this task, you will identify the resources that collectively make up a single application.

1. Sign in to the Azure portal using [https://aka.ms/AzureResiliency/regionalpreview](https://aka.ms/AzureResiliency/regionalpreview) with your assigned lab Azure credentials, or your own Azure account outside the hosted lab.
2. Open **Azure Copilot** from the top bar of the portal.
3. Select **Resiliency** from the **New chat** options.

    You can also open the Resiliency agent from the top actions on the **Resiliency** overview page.
4. Copy the following prompt into the agent chat, replace `<subscription-id>` with the ID of the subscription containing **CaldovaPayApp_Ex3_Task1**, and send it. You can find the ID under **Subscriptions → your subscription → Overview → Subscription ID** in the Azure portal.

    ```text
    Discover my application in the scope Sub: <subscription-id>, RG: CaldovaPayApp_Ex3_Task1. Use the discovery agent present under: app-discovery-ex3task1 for discovery. It already has necessary RBAC on this scope.
    ```


5. Review the resources discovered, the recommended application boundaries within the specified subscription and resource group.
6. Confirm that the discovered resources represent the application in the image below:

[caldovapayapp-architecture-single-vm.png](https://github.com/microsoft/ignite26-LAB721/blob/main/docs/caldovapayapp-architecture-single-vm.png)


> [!hint] Note that the application here has only one VM, persisting in a single zone, and a Standard PG SQL server. 


7. Verify that the expected CaldovaPayApp resources are included before continuing to Service Group creation.

> [!NOTE]
> The discovery agent already has the necessary role-based access control, or RBAC, permissions on the specified scope. You do not need to assign additional permissions as part of this exercise. If the Resiliency Agent asks about permission, prompt it to assign the necessary permissions and validate the Discovery Agent

✅ By the end of this task, you have identified the Azure resources that collectively make up the CaldovaPayApp.

> [!knowledge] This discovery can work across resource groups also at scale, making it easier for you to identify resources on Azure that make up your application


> [!note] Stay in the same Resiliency Agent chat


===

# 🛠️ Task 2: Create a Service Group for CaldovaPayApp

A Service Group allows Caldova to represent the resources supporting CaldovaPayApp as one application.

## Option 1: Create the Service Group using the Resiliency agent

1. Continue in the same Resiliency agent conversation used for application discovery.
2. Ask the agent to create a Service Group from the discovered application resources:

    ```text
    Using the application resources that were discovered, create a Service Group for CaldovaPayApp. Show me the resources that will be included and ask for confirmation before creating it.
    ```


3. Review the resources that the agent proposes adding to the Service Group.
4. Confirm that only resources belonging to the application discovered in Task 1 are included.
5. When prompted for the Service Group name, use the format `CaldovaPayApp_<unique-suffix>`. Replace `<unique-suffix>` with a unique value of your choice, for example `CaldovaPayApp_a7f29c`. Keep the actual name you choose for the remaining tasks.

6. Confirm the creation of the Service Group. 

> [!IMPORTANT]
> Service Group names must be unique. If your chosen name is already in use, choose a different suffix. In later prompts, replace `<service-group-name>` with the full name you actually created, without angle brackets.


## Option 2: Create the Service Group manually

Only use this option if Service Group creation through the Resiliency agent is unavailable.

1. Search for **Resiliency** in the Azure portal search bar and open the **Resiliency** dashboard.
2. In the left menu, expand **Infrastructure Resiliency**.
3. Select **Service Groups**.
4. Select **Create Service Group**.
5. Enter a name in the format `CaldovaPayApp_<unique-suffix>`. Replace `<unique-suffix>` with a unique value of your choice, for example `CaldovaPayApp_a7f29c`. Keep the actual name you choose for the remaining tasks.

> [!IMPORTANT]
> Service Group names must be unique. If your chosen name is already in use, choose a different suffix. In later prompts, replace `<service-group-name>` with the full name you actually created, without angle brackets.

6. Select the Tenant Root as the parent 
7. Click on 'Add Members' and select the resource group **CaldovaPayApp_Ex3_Task1**
8. Deselct the Monitoring option, skip the tags and Review the inputs on the **Review + Create** tab.
9. Complete the Service Group creation.


✅ By the end of this task, the resources supporting the pre-deployed CaldovaPayApp are represented together as an application through a Service Group.

===

# 🛠️ Task 3: Assign a Zonal and regional Resiliency Goal

Now that the resources have been grouped as an application, assign a zonal and regional resiliency goals to the Service Group.

## Step 1: Assign the zonal resiliency goal using the Resiliency agent

1. Return to the Resiliency agent.
2. Copy the following prompt, replace `<service-group-name>` with the full Service Group name you created in Task 2, and send it:

    ```text
    Assign a zonal resiliency goal to the Service Group named <service-group-name>. Show me the proposed goal and ask for confirmation before making the change.
    ```


3. Review the goal proposed by the agent.
4. Confirm the goal assignment.

## Step 2: Assign the regional resiliency goal from the Azure portal

1. Search for **Resiliency** in the Azure portal search bar and open the **Resiliency** dashboard.
2. In the left menu, expand **Infrastructure Resiliency**.
3. Select **Service Group**.
4. Locate the Service Group you created in Task 2, using its full name.
5. Review its **Regional Resiliency** goal in *Resiliency Goals* section
6. Select **Assign regional goal**.
7. Check the "Track this Service Group against regional resiliency goals" checkbox. 
    1. Note that the zonal resiliency goal is already checked on this tab because you added it from the agent in Step 1
8. Click on *Review + Assign* and wait for the goal assignment to complete
9. Navigate back to the service group overview in Resiliency and review the Regional Resiliency Insights

> [!NOTE]
> Goal assignment and resource discovery may take several minutes. If the status does not update, refresh the page before continuing.

✅ By the end of this task, CaldovaPayApp has a zonal and regional resiliency goal against which its application-level posture can be assessed.

====

# 🛠️ Task 4: Assess the Resiliency Posture of CaldovaPayApp

Now assess whether the resources supporting CaldovaPayApp collectively meet the assigned zonal and regional resiliency goal.

## Run resiliency assessments using the Resiliency agent

1. Return to the Resiliency agent.
2. Copy the following prompt, replace `<service-group-name>` with the full Service Group name you created in Task 2, and send it:

    ```text
    Show me the resiliency posture for my application <service-group-name>. Show which resources meet the assigned goal, which resources do not meet it, and the recommendations for addressing any gaps.
    ```

3. Review the agent response.

4. Identify:
    - The application's overall zone and regional resiliency status
    - The resources that meet the assigned goal
    - The resources that do not meet the assigned goal
    - The recommendations for addressing the identified gaps

5. Run a Risk assessment for the Caldova Payments application

Copy the following prompt, replace `<service-group-name>` with the full Service Group name you created in Task 2, and send it:

```text
Run an assessment for <service-group-name>. I want to understand the risks for my application's resiliency.
```

6. Review the agent's response. Expand the Assessment report and note:
    1. The Goals status
    2. Posture of the resources
    3. Risks to your application

> [!IMPORTANT]
> Do not assume that the entire application will be marked **Not Resilient**.
> 
> Review the actual status displayed in the lab environment and identify the specific resources that do not meet the assigned goal.

✅ By the end of this task, you have assessed CaldovaPayApp as an application and identified whether any supporting resources fail to meet its resiliency goal.

===

## 🔍 What to Look For

You should be able to answer the following questions:

- Does CaldovaPayApp meet its assigned zonal resiliency goal?
- Which resource or resources do not meet the goal?
- What change does Azure recommend?
- How would addressing the recommendation improve the application's resiliency posture?


✅ By the end of this task, you have identified the resiliency gaps affecting CaldovaPayApp and reviewed the recommendations available to improve its resiliency posture.

===

# ✅ Exercise Complete

In this exercise, you:

- Discovered the Azure resources that make up CaldovaPayApp within a specified subscription and resource group
- Used the provided discovery agent, which already has the necessary RBAC on that scope
- Reviewed the discovered application resources
- Grouped the resources into a Service Group
- Assigned a zonal and regional resiliency goal to the application
- Assessed the application's resiliency posture against that goal
- Identified resources that do not meet the goal
- Reviewed the recommendations available to address those resiliency gaps

You started Exercise 1 by looking at resiliency across Caldova's Azure estate.

In this exercise, you zoomed into a single application and moved through the following journey:

**Discover → Group → Set Goal → Assess → Recommend**

You now have an application-level view of CaldovaPayApp and can see where resiliency improvements are required.

===

# ➡️ Up Next: Explore Recovery plans and Drills in Resiliency Manager

Assessment helps Caldova understand where its application is vulnerable and what should be improved.

But resiliency also requires being prepared for the point when an application must be recovered.

In the optional recovery exercise, you will explore how a recovery plan can coordinate the recovery of the resources supporting CaldovaPayApp.

===

### Exercise 4 (Optional): Stay Resilient: Recovery Plan Execution

## Contents

1. [Exercise 4 (Optional): Stay Resilient: Recovery Plan Execution]
2. [Task 1: Review the recovery plan]
3. [Task 2: Review the drill]
4. [Task 3: Execute the recovery plan]

Choose **Next** to begin.

===

## Overview

Caldova's platform team has already grouped the CaldovaPayApp resources into the service group **CaldovaPayApp_Ex4_Task1_SG**, set a zonal resiliency goal for it, and created a zonal recovery plan called **CaldovaRecoveryPlan**. They have also run a drill to check that the plan works.

As the Platform Architect, you will review the plan and the drill results before the holiday surge. Then you will run the recovery plan to make sure CaldovaPayApp can be brought back in the right order if an availability zone goes down.

## Objective

Explore recovery plan and drill options in the Resiliency Manager for your service group

> [!NOTE]
> This is an exploratory exercise

===

### 🛠️ Task 1: Review the Recovery Plan

1. Search for **Resiliency** in the portal search bar and open the Resiliency dashboard.

2. In the left menu, expand **Infrastructure Resiliency** and select **Service Group**.

3. Open the Service Group you created in Exercise 3, using its full name. In the left menu, select **Recovery Plans**.

5. Try creating a recovery plan

6. Confirm that the CaldovaPayApp resources are included in the plan. 
    1. Review the **recovery groups** and the order in which they will run.
    2. Review the protected and unprotected resources
    3. Try excluding or including a resource

7. Note, you will not have enough time to run the recovery plan. THis is purely exploratory. 
    1. You can also ask the agent to create a recovery plan for the Service Group you created in Exercise 3. Include its full name in your request.

> [!NOTE]
> Resources configured with a Highly Available (HA) solution are automatically excluded, because they perform self-managed failover. 

✅ By the end of this task, you have explored Caldova's zonal recovery plan options. 

===

### 🛠️ Task 2: Review the Drill

1. In the left menu under **Infrastructure Resiliency**, select **Drills**.

2. Create a drill for the Service Group you created in Exercise 3, using its full name.

3. Review the drill resources and fault designer:

    - Which resources are automatically included
    - Any issues or warnings the drill found
    - Which resources have a native fault support and which ones need a custom fault

🔍 Example: The drill helps Caldova validate that the recovery plan works before a real zonal outage happens. Did any recovery group take longer than expected or raise a warning that should be fixed before the holiday surge? That way, Caldova can **Stay Resilient**. 

✅ By the end of this task, you have understood that the Resiliency Manager and Agent can help Caldova create and manager recovery plans and resiliency drills helping Caldova validate their resiliency posture.

===

## 🎉 Congratulations!

You have completed the **Hands-on with Resiliency in Azure: Assess, Recommend, Recover** lab.

By the end of this lab, Caldova has:

- 🏗️ Deployed CaldovaPayApp from an IaC template with zonal resiliency built in from the start.
- ✅ Backed up its cloud-native workloads in a vault hardened against ransomware.
- 🛡️ Learned to identify compromised recovery points and recover virtual machines in bulk from verified clean snapshots.
- 🌐 Grouped its application resources, assessed them against zonal and regional resiliency goals, and remediated them.
- 🔁 Explored the Drills and Recovery plans to validate Resiliency posture and Stay Resilient

Caldova is ready for the holiday surge, and ready to recover if something goes wrong.
