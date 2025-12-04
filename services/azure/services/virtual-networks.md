# Azure Virtual Networks

An Azure Virtual Network (VNet) enables secure communication between Azure resources, on-premises environments, and the internet. At BBI we are mainly using VNets in combination with NAT gateways, so that we have a single outbound IP htat can be used for whitelising.

## Setup

### Basics

1. In the Azure Portal, create a new Virtual Network under the appropriate resource group. Typically, this should be a shared resource group (e.g., `rg-shared`).
2. Name the virtual network clearly, such as `vnet-shared`.
3. Select the correct region (e.g., West Europe) to align with your resources.

### Security

No changes are required under the Security tab during initial setup.

### IP Addresses

You can define subnets during VNet creation, but this step is optional and can be done later. When creating subnets, use clear naming conventions (e.g., `snet-terstal-webapp-prod`).

### Tags

Add tags only if necessary for resource management.

## Subnets

Subnets are segments within a VNet that allow you to organize and secure resources.

### Configuration

-   Name subnets using a clear convention, such as `snet-terstal-webapp-prod`.
-   Use IPv4 address space and allocate a /24 subnet size (e.g., `10.0.1.0/24`) for most workloads.
-   You can associate a subnet with a NAT Gateway for outbound internet access, either during creation or later.

## Integrations

### Container App Environment

A Container App Environment in Azure can be associated one-to-one with a subnet. This enables secure, private networking for containerized workloads. If the subnet is connected to a NAT Gateway, the outbound IP address for the container app environment will be static. This allows you to provide a consistent IP address to customers for whitelisting purposes.
