# Chaper 3: Storage

Azure Storage is Azure’s main, general-purpose data storage service. 
It offers native integration with key Azure services such as 

- Azure Active Directory
- Azure Key Vault
- managed identities
- Azure Functions
- Azure Logic Apps
- virtual machine disks
- Azure Cognitive Search
- Event Grid
- Azure Synapse Analytics.  

Infinite scaling capabilities make it a great choice for 
storing big data, telemetry, logfiles, images, media files, 
and both unstructured and NoSQL data.

Azure Storage offers the following services: blobs, files, queues, tables, and disks.  
VM disks are stored as blob objects.  
In this chapter, you will use the Azure Storage services to configure 
a secure, reliable, and affordable data store in your Azure subscription.  

Use Azure Storage to:

- Automatically invoke an Azure Function when a new file is added to your Azure Storage
- Index your blob files and build content search APIs for them using Azure Cognitive Search
- Store big data to be analyzed by Azure Databricks or Azure Synapse Analytics
- Use Azure Files to implement traditional SMB (Server Message Block protocol) file shares for your Windows or Linux workstations

## Using Azure Key Vault Keys to Configure Azure Storage Encryption at Rest

We need to use CMK (customer-managed keys) to encrypt your Azure Storage data at rest.

### Solution

Create a new encryption key in Azure Key Vault and configure Azure Storage to use it instead of the default Microsoft-managed keys.

### Discussion

Encryption for data at rest is automatically enabled for all Azure storage account instances. 
By default, the encryption key is managed by Microsoft.

However, whether due to security standards, commitments, or for compliance 
reasons, your organization might want to be in charge of the storage account encryption keys by creating its own keys. You can use this recipe to create your own Key Vault encryption key. This key is stored in the Azure Key Vault, and you are responsible for managing and maintaining its health and availability. If you don’t have specific 
security commitments or compliance needs, it’s fine to use the default Microsoft-managed keys. This approach has less administrative overhead for your team.

Keep in mind that when customer-managed keys are enabled for your storage account, Azure Storage queues and tables are not automatically protected by those keys. If needed, you can configure these services to be included in the CMK encryption when you create your storage account. See the Azure documentation for details.

## Controlling Azure Storage Network Access

You need to limit Azure storage account network access to one or more Azure VNets.

### Solution

Make sure the Public Network Access setting is enabled for your storage account. Then define a network access rule to permit traffic from one or more Azure VNets.

### Discussion

There are three different network access scenarios for an Azure storage account:

- Allow traffic from all public and private networks (including the internet)
- Allow traffic only from specific Azure VNets
- Allow traffic only from private endpoints with no public network access

The first option is the default behavior when you create a new storage account, unless you explicitly configure other network access settings.
In this recipe, we covered the second option, which allows traffic from one or more VNets. Keep in mind that in this case the traffic still goes through the public internet.
If you need your traffic to only go through Azure’s private backbone network, you need to choose the third option to configure private endpoints. Check the Azure Storage networking documentation for details.

### Documentation

- [Virtual Network service endpoints](https://learn.microsoft.com/en-us/azure/virtual-network/virtual-network-service-endpoints-overview)
- [What is private endpoint](https://learn.microsoft.com/en-us/azure/private-link/private-endpoint-overview)
- [Configure Azure Storage firewalls and virtual networks](https://learn.microsoft.com/en-us/azure/storage/common/storage-network-security?tabs=azure-portal)

## Granting Limited Access to Azure Storage Using SAS Tokens

You need a way to grant granular access to Azure Storage services.

### Solution

Instead of Azure Storage Keys, which grant full access, generate shared access signature (SAS) tokens with the desired access and share them with client applications and users.
