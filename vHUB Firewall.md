# Creating Azure vHub, Azure Firewall, and Firewall Manager Documentation

## Table of Contents
1. Introduction
2. Prerequisites
3. Creating an Azure Virtual WAN (vHub)
   - 3.1. Sign in to the Azure Portal
   - 3.2. Create a Virtual WAN Resource
   - 3.3. Create a vHub
   - 3.4. Add Virtual Networks to the vHub
4. Creating an Azure Firewall
   - 4.1. Sign in to the Azure Portal
   - 4.2. Create an Azure Firewall Resource
   - 4.3. Configure Firewall Rules
5. Implementing Azure Firewall Manager
   - 5.1. Sign in to the Azure Portal
   - 5.2. Create a Firewall Manager Policy
   - 5.3. Associate Firewall Policy with Firewall Instances
6. Conclusion

## 1. Introduction
This documentation provides a step-by-step guide to creating an Azure Virtual WAN (vHub), deploying an Azure Firewall, and implementing Azure Firewall Manager to centrally manage and enforce firewall policies across multiple Azure Firewall instances.

## 2. Prerequisites
Before you proceed, ensure you have the following prerequisites:

- An Azure subscription with sufficient permissions to create and manage resources.
- Basic understanding of Azure networking concepts, including Virtual Networks, Subnets, and Virtual WAN.

## 3. Creating an Azure Virtual WAN (vHub)

### 3.1. Sign in to the Azure Portal
1. Open your web browser and navigate to https://portal.azure.com.
2. Sign in with your Azure account credentials.

### 3.2. Create a Virtual WAN Resource
1. In the Azure Portal, click on "Create a resource" and search for "Virtual WAN."
2. Click on "Virtual WAN" from the search results.
3. In the "Virtual WAN" blade, click on the "+ Add" button.
4. Provide the required details for the Virtual WAN, such as:
   - **Subscription**: Select the subscription for the Virtual WAN.
   - **Resource group**: Choose an existing resource group or create a new one.
   - **Name**: Enter a unique name for the Virtual WAN.
   - **Region**: Select the region where the Virtual WAN should be deployed.
   - **Hub type**: Choose "Standard" as the hub type.
5. Click "Review + create" to validate your settings, and then click "Create" to create the Virtual WAN.

### 3.3. Create a vHub
1. In the Azure Portal, navigate to the newly created Virtual WAN resource.
2. In the "Overview" blade, click on "Virtual hubs" in the left-hand menu.
3. Click on "+ Add" to create a new vHub.
4. In the "Create virtual hub" page, provide the following details:
   - **Name**: Enter a unique name for the vHub.
   - **Hub Virtual Network**: Select the Virtual Network to which the vHub will connect.
   - **Hub Subnet**: Choose the subnet within the selected Virtual Network for the vHub.
   - **Address space**: Define the address space for the vHub in CIDR notation.
   - **SKU**: Choose the desired SKU for the vHub (e.g., Standard, HighPerformance).
5. Click "Create" to create the vHub.

### 3.4. Add Virtual Networks to the vHub
1. In the Azure Portal, navigate to the Virtual WAN resource and select the vHub you created.
2. In the "Overview" blade of the vHub, click on "Virtual network connections" in the left-hand menu.
3. Click on "+ Add" to add a new Virtual Network connection to the vHub.
4. In the "Add virtual network connection" page, provide the following details:
   - **Virtual network**: Select the Virtual Network you want to connect to the vHub.
   - **Subscription**: Choose the subscription of the Virtual Network.
   - **Resource group**: Select the resource group of the Virtual Network.
   - **Subscription**: Choose the subscription of the Virtual Network.
   - **Resource group**: Select the resource group of the Virtual Network.
   - **Use VPN Gateway**: Choose whether to use VPN Gateway (enabled by default).
   - **VPN Site Configuration**: Configure the VPN site settings if VPN Gateway is used.
   - **Security Type**: Choose the security type for the connection (ExpressRoute or VPN).
   - **Connection type**: Choose the type of connection (e.g., Site-to-Site, Point-to-Site).
5. Click "OK" to add the Virtual Network connection to the vHub.
6. Repeat steps 3-5 to add more Virtual Networks to the vHub if needed.

## 4. Creating an Azure Firewall

### 4.1. Sign in to the Azure Portal
1. Open your web browser and navigate to https://portal.azure.com.
2. Sign in with your Azure account credentials.

### 4.2. Create an Azure Firewall Resource
1. In the Azure Portal, click on "Create a resource" and search for "Firewall."
2. Click on "Azure Firewall" from the search results.
3. In the "Azure Firewall" blade, click on the "+ Add" button.
4. Provide the required details for the Azure Firewall, such as:
   - **Subscription**: Select the subscription for the Azure Firewall.
   - **Resource group**: Choose an existing resource group or create a new one.
   - **Name**: Enter a unique name for the Azure Firewall.
   - **Region**: Select the region where the Azure Firewall should be deployed.
   - **Virtual WAN**: Choose the Virtual WAN you created earlier.
   - **Public IP Address**: Create a new Public IP Address resource or select an existing one.
5. Click "Review + create" to validate your settings, and then click "Create" to deploy the Azure Firewall.

### 4.3. Configure Firewall Rules
1. In the Azure Portal, navigate to the newly created Azure Firewall resource.
2. In the "Overview" blade, click on "Firewall rules" in the left-hand menu.
3. Click on "+ Add" to create a new Firewall rule.
4. In the "Add rule" page, provide the following details:
   - **Name**: Enter a descriptive name for the rule.
   - **Priority**: Set the priority for the rule. Lower values have higher priority (1 being the highest).
   - **Rule Type**: Choose the rule type (Application rule, Network rule, or NAT rule).
   - **Rule Action**: Choose whether to allow or deny traffic matching this rule.
   - **Rule Name**: Provide the specific rule details, depending on the rule type selected.
   - **Rule Collection**: If needed, assign the rule to a specific rule collection.
5. Click "Add" to create the Firewall rule.
6. Repeat steps 3-5 to add more Firewall rules if needed.

## 5. Implementing Azure Firewall Manager

### 5.1. Sign in to the Azure Portal
1. Open your web browser and navigate to https://portal.azure.com.
2. Sign in with your Azure account credentials.

### 5.2. Create a Firewall Manager Policy
1. In the Azure Portal, click on "Create a resource" and search for "Firewall Manager."
2. Click on

 "Firewall Manager" from the search results.
3. In the "Firewall Manager" blade, click on the "+ Add" button.
4. Provide the required details for the Firewall Manager Policy, such as:
   - **Subscription**: Select the subscription for the Firewall Manager Policy.
   - **Resource group**: Choose an existing resource group or create a new one.
   - **Name**: Enter a unique name for the Firewall Manager Policy.
   - **Region**: Select the region where the Firewall Manager Policy should be deployed.
5. Click "Review + create" to validate your settings, and then click "Create" to create the Firewall Manager Policy.

### 5.3. Associate Firewall Policy with Firewall Instances
1. In the Azure Portal, navigate to the Firewall Manager Policy you created.
2. In the "Overview" blade, click on "Azure Firewall instances" in the left-hand menu.
3. Click on "+ Add" to associate a new Firewall instance with the policy.
4. In the "Add firewall instance" page, provide the following details:
   - **Subscription**: Select the subscription of the Firewall instance.
   - **Resource group**: Choose the resource group of the Firewall instance.
   - **Firewall**: Select the Azure Firewall resource to associate with the policy.
   - **Region**: Choose the region of the Firewall instance.
5. Click "Add" to associate the Firewall instance with the Firewall Manager Policy.
6. Repeat steps 3-5 to associate more Firewall instances with the policy if needed.

## 6. Conclusion
Congratulations! You have successfully created an Azure Virtual WAN (vHub), deployed an Azure Firewall, and implemented Azure Firewall Manager to centrally manage and enforce firewall policies. By following these steps, you can efficiently secure your Azure network and applications while gaining centralized control over firewall management.