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

## Securing Azure Virtual Networks with Azure Firewall

You need to improve your Azure network infrastructure security by forwarding all the egress subnet traffic to Azure Firewall.

### Solution

Provision a new Azure Firewall resource and use a route table to forward all the egress subnet traffic to the Azure Firewall.

### Discussion

In this recipe, we used Azure Firewall to inspect egress traffic from an Azure VNet subnet. By default, all traffic is blocked unless there is a matching firewall rule for it. See the Azure Firewall rule processing logic documentation for details. As you saw, there are three sets of Azure Firewall classic rules:

**DNAT rules**

For inbound traffic into your subnets. DNAT rules will be processed first.

**Network rules**

For outgoing traffic from your subnets. You can allow or block traffic based on IP address and port number. Network rules are processed after DNAT rules.

**Application rules**

Finally, if you need to allow outgoing traffic for HTTP, HTTPS, or MSSQL protocols, use these rules. Application rules are processed last.

> You can optionally use an Azure Firewall Policy instead of directly defining rules in the Azure Firewall resource. This policy can then be assigned to one or more Azure Firewall instances.

Azure Firewall also offers threat intelligence-based filtering to alert and/or deny traffic from Microsoft’s list of malicious IP addresses, fully qualified domain names, and URLs.

## Securing Azure Virtual Networks with Network Security Groups

We need to improve network security by controlling inbound and outbound subnet traffic.

### Solution

Provision a new Azure network security group (NSG) resource and assign it to your subnets.

By default, all traffic is blocked by Azure NSGs. 
Using NSG security rules, we can allow or deny both inbound (ingress) and outbound (egress) subnet traffic. 
The priority can be between 100 and 4096. Rules with lower numbers have higher priority and will be processed first. 
Imagine we deployed a web server Azure VM into our subnet and so need to allow for inbound traffic on  ports 80 and 443.

### Discussion

In this recipe, we created a new NSG and assigned it to a subnet. 
NSGs provide basic protection based on source and destination IP address and port numbers. 
One NSG can be assigned to multiple subnets, but each subnet can have only one NSG assigned.

In “Securing Azure Virtual Networks with Azure Firewall”, we set up Azure Firewall, which is a more sophisticated service. 
We can use NSGs along with Azure Firewall to provide extra protection for your subnets. 
If unwanted traffic goes through one, the next will block it, providing defense in depth for our Azure network.

## Connecting Two Azure VNets Using Azure Network Peering

You want resources in two separate Azure VNets configured so that they will be able to communicate with each other.

### Solution

Create two new Azure network peering resources between your two Azure VNets, so that the resources in the two  VNets can see one another.

> **Important:**  
> To create network peering, an account should have the Network Contributor role assigned over both Azure VNets.

## Verifying Azure VNet Connectivity Using Azure Network Watcher

You need to monitor or verify network connectivity between an Azure VM 
and other destinations, such as the internet or another VM.

### Solution

Create an Azure Network Watcher connection monitor and use it to verify connectivity between your IaaS (infrastructure as a service) endpoints.

### Discussion

> **Important:**
> Azure Network Watcher is only intended for IaaS resources such as Azure VMs. 
> This service does not support Azure PaaS (platform as a service) services such as App Services as the source resource.

### Documentation

[What is Azure Network Watcher?](https://learn.microsoft.com/en-us/azure/network-watcher/network-watcher-overview)

