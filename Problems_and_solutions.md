# Problems & Solutions

---

# Chapter 1: Security

It provides methods to improve the security of Azure resources through RBAC and network firewalls.

## Connecting to a Private Azure Virtual Machine Using Azure Bastion

You need to connect to an Azure virtual machine using RDP or SSH. Your Azure virtual machine (VM) is a private VM, meaning it does not have a public IP address.

### Solution

Deploy an Azure Bastion host resource to the same virtual network (VNet) as your Azure VM. Then, you can use SSH or RDP to access your Azure VM. A private Azure VM has no public IP address, making it invisible to the public internet. See the solution architecture diagram in Figure 1-5.”

> **Important:**
> Exposing a VM via a public IP address is never a good idea.

## Protecting Azure VM Disks Using Azure Disk Encryption

You need to encrypt your Azure VM disks using BitLocker or dm-crypt to protect your data or meet your company’s security and compliance standards.

### Solution

Create an encryption key in Azure Key Vault, and use it to configure BitLocker (Windows VM) or dm-crypt (Linux VM) encryption for your Azure VMs”

## Blocking Anonymous Access to Azure Storage Blobs

You need to prevent developers from accidentally granting anonymous public access to Azure Storage blobs and containers.

### Solution

Set the --allow-blob-public-access flag to false programmatically, or set the “Allow Blob public access” field to Disabled in the Azure portal (see Figure 1-11). This can be set for both new and existing storage accounts.

## Configuring an Azure Storage Account to Exclusively Use Azure AD Authorization

You want to prevent an Azure storage account from accepting storage keys and SAS tokens for authorization. Doing this leaves users with the more secure Azure AD authentication/authorization method.

### Solution

Set the --allow-shared-key-access flag to false programmatically, or set the “Allow storage account key access” field to Disabled in the Azure portal (see Figure 1-12). This can be configured for both new and existing storage accounts.

### Documentation

- [Authorize access to data in Azure Storage](https://learn.microsoft.com/en-us/azure/storage/common/authorize-data-access)

## Storing and Retrieving Secrets from Azure Key Vault

You need to safely store and retrieve passwords, database connections, and other sensitive data in Azure.

### Solution

Store your secrets, keys, and certificates in the Azure Key Vault service. Give access to clients to read the secrets from the Key Vault when needed.

## Enabling Web Application Firewall (WAF) with Azure Application Gateway 

You need to protect your Azure web applications from common web attacks such as SQL injection.

### Solution

Deploy an Azure Application Gateway resource in front of your web application, and enable WAF on it.

**WAF protects your web applications against common web attacks such as:**

- SQL injection
- Cross-site scripting
- Command injection
- HTTP request smuggling
- HTTP response splitting
- Remote file inclusion
- HTTP protocol violations

Check the [WAF features documentation](https://learn.microsoft.com/en-us/azure/web-application-firewall/ag/ag-overview) for a complete list of supported features.

> **Note:**  
> WAF is one of the Azure Application Gateway features. 
> Azure Application Gateway is a web load balancer with a rich set of capabilities. 
> Setting up an Azure Application Gateway involves creating HTTP listeners, routing rules, etc. 
> See [Application Gateway CLI documentation](https://learn.microsoft.com/en-us/azure/application-gateway/redirect-http-to-https-cli) for details.

### Documentation

- [Azure Web Application Firewall (WAF) policy overview](https://learn.microsoft.com/en-us/azure/web-application-firewall/ag/policy-overview)

# Chapter 2: Networking

It reviews Azure Virtual Network (VNet) security, routing, and monitoring.

# Chapter 3: Storage

It provides recipes for Azure storage accounts, 
enabling us to optimize cost, secure  data, and protect it against accidental deletion.

# Chapter 4: Persisting Data

It provides guidelines to configure and protect 
the main Azure relational and NoSQL databases, Azure SQL and Azure Cosmos DB.

# Chapter 5: Messaging and Events

It enables us to set up reliable messaging between services and solutions using Azure’s messaging suite of services.

# Chapter 6: Big Data

It introduces Azure services, including Azure Stream Analytics, Azure Synapse Analytics, 
Azure Databricks, and Azure Data Factory, designed to mine insights from your big data.

# Chapter 7: Azure Functions and Serverless Services

It provides recipes to implement microservices using Azure Function Apps.

# Chapter 8: Azure App Service

It provides recipes to configure autoscaling, secure network access, and deploy App Services using several methods.

# Chapter 9: Containers

It introduces Azure services designed to host and run containerized applications in Azure.

# Chapter 10: Azure Cognitive Services

It helps us develop smart applications by using Azure Cognitive Services.  
Recipes in this chapter enable us to gain insights from images, audio, and text content using AI-backed services.

# Chapter 11: Management and Monitoring

It introduces tools to monitor and control Azure service costs and then reviews Azure Monitor platform logs.
