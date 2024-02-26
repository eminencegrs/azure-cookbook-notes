# Chapter 2: Networking

Every Azure service needs the right network connectivity to securely communicate with other dependencies and service clients. 
The processed data should be fed to downstream services over a secure connection. 
To reduce the attack surface, services such as Azure Cosmos DB need to limit the incoming requests to desired networks only. 
Microservices deployed to Azure Functions, Azure Kubernetes Service, 
or Azure Container Instances need to connect to one another in an efficient and secure manner. 
These are just a few examples of the hundreds of services that are available. 
Under the hood, these communications are achieved using Azure networking infrastructure. 
At the core of this infrastructure sits **Azure Virtual Network**.

## Creating an Isolated Private Network by Provisioning an Azure Virtual Network

You need to create an isolated private network in Azure to protect your resources 
from requests originated from unwanted networks and IP addresses.

### Solution

Provision an Azure Virtual Network (VNet), create one or more subnets in it, 
and place your resources, such as Azure VMs, in the desired subnets.

### Discussion

Azure VNet is the building block of a private network in the Azure cloud.  
Azure resources (VMs, App Services, Function Apps, etc.) use Azure VNets 
to securely communicate with each other, the internet, and even on-premises (local) networks.

Many Azure resources support virtual network integration. 
Use the virtual network integration feature to isolate those resources from public networks and the internet. 
For instance, we can configure a Cosmos DB database to accept requests only from a specific Virtual network. 
This protects our database from unwanted clients and attackers, and improves our Azure subscription security posture.
