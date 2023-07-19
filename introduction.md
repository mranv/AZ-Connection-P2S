# Introduction

This document serves as comprehensive data documentation for the IP Address Retrieval System. The system is designed to handle two types of users, User 1 and User 2, each with different connection configurations and IP address retrieval methods. The system allows users to obtain their respective IP addresses by searching for "whatsmyipaddress." This documentation aims to provide clarity, conciseness, and accuracy to both technical and non-technical readers.

## **User Types and Connection Configurations**

User 1:
- Connection: User 1 connects to the internet through a local ISP provider.
- IP Address: User 1 is assigned an IP address (y.y.y.y) by the local ISP provider.

User 2:
- Connection: User 2 connects to the internet using a VPN configuration file.
- VPN Configuration: The VPN configuration is created in Virtual WAN and consists of a Virtual Hub.
- Firewall and Custom DNS Servers: The VPN configuration includes a firewall that acts as custom DNS servers.
- Public IP Address: The firewall's public IP address is (x.x.x.x).

![Example SVG](./Internet2.svg)



# **Brief About the Document**
This document aims to provide a detailed overview of the Custom Topology used above, including its functionalities and various components. Whether you are a technical expert or a non-technical user, this documentation strives to offer clarity, conciseness, and accuracy, enabling you to understand and utilize the system effectively.

## Overview of the IP Address Retrieval System

The IP Address Retrieval System is a sophisticated tool designed to cater to two distinct user types: User 1 and User 2. Each user type has different connection configurations and methods for IP address retrieval.

### User 1

User 1 is characterized by their connection to the internet through a local Internet Service Provider (ISP) provider. When User 1 accesses the internet, the ISP assigns them a unique IP address (y.y.y.y). This IP address serves as the identifier for User 1's device on the internet, allowing them to communicate with other devices and access online resources.

### User 2

On the other hand, User 2 follows a different connection approach. They access the internet using a Virtual Private Network (VPN) configuration file. The VPN setup is created within a Virtual WAN (Wide Area Network) environment and incorporates a Virtual Hub. This configuration enhances User 2's online security and privacy, as it routes their internet traffic through the VPN.

Moreover, the VPN configuration also includes a firewall that acts as custom Domain Name System (DNS) servers. DNS plays a critical role in translating human-readable domain names (like www.example.com) into machine-readable IP addresses. In this case, the firewall takes on the responsibility of managing DNS requests for User 2's internet traffic.

The firewall in the VPN configuration is assigned a public IP address (x.x.x.x). This public IP address is the outward-facing address that other devices and servers on the internet use to identify User 2's VPN connection. It acts as a gateway between the secure VPN network and the external internet.

## IP Address Retrieval Functionality

To retrieve their respective IP addresses, both User 1 and User 2 can make use of the "whatsmyipaddress" search feature within the IP Address Retrieval System. This functionality ensures that users can easily and conveniently access their assigned IP addresses, whether they are connected through a local ISP or a VPN configuration.

## Technical Documentation

Throughout this documentation, we will delve into the technical intricacies of the system, providing step-by-step guides for users of all levels of expertise. By the end of this document, you should have a comprehensive understanding of the IP Address Retrieval System and be equipped to utilize it effectively based on your specific connection configuration and user type.

Let's now embark on this journey of exploration into the inner workings of the IP Address Retrieval System. Thank you for using our system!

### *Please note that this documentation is written in English & the provided information is written in Markdown format.*
