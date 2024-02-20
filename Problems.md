# Problems

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
