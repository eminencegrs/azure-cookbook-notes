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

We need to create an isolated private network in Azure to protect your resources 
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

## Creating a Network Layout in Azure Virtual Networks Using Subnets

We want to divide your Azure VNet into several subnetworks (subnets) for organization, 
and security. Later you will deploy Azure resources into these subnets.

### Solution

Create one or more subnets in your Azure VNet. 
Then, multiple resources can be placed into these subnets.

### Discussion

Azure subnets are the main Azure network security pillar. 
Resources such as VMs should be deployed to an Azure subnet. 
Other Azure resources, such as Azure App Service Environment, 
Azure API Management, Azure Functions Premium, and more 
can be deployed to subnets. 
Almost all Azure network security services such as Azure Firewall, 
network security groups (NSGs), and Azure route tables 
are designed to work with Azure subnets.

Before creating a new subnet in your VNet, 
make sure you know which IP ranges are already taken by existing subnets, 
and choose the next available free range. 
Subnets within the same Azure VNet can’t have any overlapping address. 
You can resize deployed Azure subnets, 
if there is available growing space in the parent VNet. 
It is a good practice to understand how big your subnet needs to be 
and allocate the right address space in the first place.

## Routing Network Traffic Using User-Defined Routes

You need to route outgoing subnet traffic to Azure and/or on-premises networks and/or internet resources.

### Solution

Create an Azure route table, add one or more custom routes to it, and associate the new route table with your subnets.

### Discussion

Microsoft Azure automatically creates a system (default) route table for each subnet and adds system default routes to it. You can’t update or delete these routes, but you can override them. In this recipe, you learned how to override these system routes by creating and assigning a custom route table.

One of the main use cases for custom routes (route tables) is to forward all the outgoing subnet traffic to a virtual appliance such as the Azure Firewall service. This enables you to monitor, secure, and limit the subnet traffic.

