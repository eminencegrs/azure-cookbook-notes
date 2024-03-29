# Chapter 1: Security

It provides methods to improve the security of Azure resources through RBAC and network firewalls.

> **Important:**  
> Cloud security is a common responsibility shared between Microsoft Azure and a customer/consumer.
> It is our responsibility to correctly configure resource security.

## Creating a New User in Your Azure Account

The Owner (administrator) account has far more permissions than are needed for everyday development tasks.  
We need to create a new user account for a developer with just enough permissions to complete assigned tasks.

### Solution

First, we need to create a new user in our Azure Active Directory (Azure AD).  
Then assign the Contributor role-based access control (RBAC) role to that user, 
so enough permissions are assigned without granting this user the same permission level as the Owner.

## Creating a New Custom Role for Our User

We need to grant a limited set of permissions to a user, group, or Azure AD principal.  
There is no built-in Azure RBAC role that offers these exact permissions.

### Solution

First create a custom Azure role, then assign the role to the users, groups, or principals.

### Discussion

Custom roles are perfect for situations in which we need to assign exactly the right amount of permissions to a user.  
Access to multiple services can also be granted using custom roles.  
The role definition JSON files can be stored in a source control system and 
deployed using Azure CLI, Azure PowerShell, or even ARM templates.  
We can assign multiple RBAC roles to a user or group.  
Our test user has both Contributor and Custom Storage Data Reader assigned.  
In real-world scenarios, we will need to remove the Contributor role from a user, 
because it gives many more permissions compared to the custom role.

## Assigning Allowed Azure Resource Types in a Subscription

WE need to limit the Azure resource types that subscription users can create.

### Solution

Assign the "Allowed resource type" **Azure Policy** to

- **the management group**,
- **subscription**,
- or **resource group** scopes

with the list of allowed resource types as the policy parameter.

## Assigning Allowed Locations for Azure Resources

We need to limit the locations (regions) Azure resource can be provisioned in.

### Solution

Assign the "Allowed locations" policy to the **management group**, **subscription**, or *resource group**, 
with the list of allowed Azure regions as the policy parameter.

## Discussion

Many countries and regions have data residency laws in effect.  
This means the user data should not leave its geographical jurisdiction.  
The EU’s General Data Protection Regulation (GDPR), 
which prohibits EU residents’ data leaving EU boundaries, is an example of such a law.  
The “Allowed locations” Azure policy is the perfect tool to enforce compliance to standards such as GDPR.

## Connecting to a Private Azure Virtual Machine Using Azure Bastion

We need to connect to an Azure virtual machine using RDP or SSH. 
Our Azure virtual machine (VM) is a private VM, meaning it does not have a public IP address.

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

Set the `--allow-blob-public-access` flag to false programmatically, 
or set the "Allow Blob public access" field to Disabled in the Azure portal.  
This can be set for both new and existing storage accounts.

## Configuring an Azure Storage Account to Exclusively Use Azure AD Authorization

You want to prevent an Azure storage account from accepting storage keys and SAS tokens for authorization. 
Doing this leaves users with the more secure Azure AD authentication/authorization method.

### Solution

Set the `--allow-shared-key-access` flag to false programmatically, 
or set the "Allow storage account key access" field to Disabled in the Azure portal.  
This can be configured for both new and existing storage accounts.

### Discussion

Azure storage accounts support multiple authorization methods, which fall into two groups:

- **Key-based access**, such as using storage account keys, or SAS tokens
- **Azure Active Directory** access using an Azure AD principal, user, or group, and an RBAC role

Some organizations prefer the second method, because no password, account key, or SAS token needs 
to be stored or maintained, resulting in a more secure solution.

### Documentation

- [Authorize access to data in Azure Storage](https://learn.microsoft.com/en-us/azure/storage/common/authorize-data-access)

## Storing and Retrieving Secrets from Azure Key Vault

We need to safely store and retrieve passwords, database connections, and other sensitive data in Azure.

### Solution

Store our secrets, keys, and certificates in the Azure Key Vault service.  
Give access to clients to read the secrets from the Key Vault when needed.

## Enabling Web Application Firewall (WAF) with Azure Application Gateway

We need to protect our Azure web applications from common web attacks such as SQL injection.

### Solution

Deploy an Azure Application Gateway resource in front of our web application, and enable WAF on it.

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
