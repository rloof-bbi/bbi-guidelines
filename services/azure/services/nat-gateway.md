# Azure NAT Gateway

An Azure NAT Gateway provides outbound internet connectivity for resources in a virtual network, using a static public IP address. At BBI, the main use case for NAT Gateway is to provide a consistent outbound IP for whitelisting.

## Setup

### Basics

1. In the Azure Portal, create a NAT Gateway in an appropriate resource group, typically a shared one (e.g., `rg-shared`).
2. Name the NAT Gateway clearly, such as `ng-shared`.

### Outbound IP

1. Create a new Public IP address resource and give it a clear name (e.g., `pip-shared`).
2. Public prefixes can be left empty.

### Subnet

You can associate the NAT Gateway with one or more subnets. This can be done during setup or later, as long as the subnets exist.

### Tags

Add tags only if necessary for resource management or cost tracking.
