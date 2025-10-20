**Azure Subscriptions:**
<img width="520" height="220" alt="image" src="https://github.com/user-attachments/assets/fa7aba84-ada3-4706-b9a6-d126b1876776" />

**Azure management groups**
If you have many subscriptions, you might need a way to efficiently manage access, policies, and compliance for those subscriptions. Azure management groups provide a level of scope above subscriptions. You organize subscriptions into containers called management groups and apply governance conditions to the management groups.
<img width="608" height="376" alt="image" src="https://github.com/user-attachments/assets/fffbd156-3b3b-42ad-943a-9f95fece2527" />
Important facts about management groups:

10,000 management groups can be supported in a single directory.
A management group tree can support up to six levels of depth. This limit doesn't include the root level or the subscription level.
Each management group and subscription can support only one parent.

**Azure VMS:**
- Single VM for simple dev tasks.
- Can scale this using Azure VM **Virtual machine scale sets** Similar to autoscaling.
- There is azure **virtual machine availability sets** . This is for high availability

**Create Resource Group** : az group create --name IntroAzureRG --location eastus
**Create VM command** : 
az vm create --resource-group "IntroAzureRG" --name my-vm --size Standard_D2s_v5 --public-ip-sku Standard --image Ubuntu2204 --admin-username azureuser --generate-ssh-keys

az vm extension set - This command is used to install extensions

**Azure Containers**
- Docker
- Kubernetes

**Azure Functions**
Azure VMs and containers need to be running even when you dont require them. Azure Functions are used only when u require them to run. No need to mainten like VMs and Containers. Key components to serverless computing

**App hosting options**
- Azure VMs
- Azure Containers
- Azure App Services(Devendra did it for hosting MCP server, MCP client as fast api apps):
    - Web apps
    - API apps
    - Webjobs
    - Mobile apps

**Azure Virtual Networking**
**Isolation and segmentation**
**Internet communications**
**Communicate between Azure resources**
**Communicate with on-premises resources** -- VPN, Express route(dedicated route)
**Route network traffic** - Route Tables(Rules how traffic should travel over n/w), Border Gateway protocol(works with Azure VPN gateways, Azure Route Server, or Azure ExpressRoute to propagate on-premises BGP routes to Azure virtual networks)
**Filter network traffic** - Network security groups are Azure resources that can contain multiple inbound and outbound security rules. You can define these rules to allow or block traffic, based on factors such as source and destination IP address, port, and protocol.
Network virtual appliances are specialized VMs that can be compared to a hardened network appliance. A network virtual appliance carries out a particular network function, such as running a firewall or performing wide area network (WAN) optimization.
**Connect virtual networks**- Peering allows 2 vpns to communicate with each other

**Commands**
az network nsg list  --> List network security group rules
az network nsg rule list --> Will give rule list for a specific nsg 
az network nsg rule create --> Create nsg rule

**Azure Virtual Private Networks**
Azure Virtual Private Networks (VPNs) provide secure, encrypted communication between networks over the public internet. They are commonly used to connect:
On-premises datacenters to Azure (site-to-site)
Individual devices to Azure (point-to-site)
One Azure virtual network to another (network-to-network)
**VPN Gateway**
An Azure VPN Gateway is deployed in a dedicated subnet and handles encrypted traffic. Only one gateway is allowed per virtual network, but it can connect to multiple sites.
**VPN Types**
Policy-based VPN: Uses static IP rules to decide which traffic to encrypt.
Route-based VPN (preferred): Uses routing tables and virtual interfaces; better for complex, dynamic environments.
**Use Route-based VPN for:**
VNet-to-VNet
Point-to-site
Multisite
ExpressRoute coexistence
High availability
High Availability Options
Active/Standby: Two instances (one backup), auto failover in seconds (planned) or ~90 seconds (unplanned).
Active/Active: Uses BGP, both instances handle traffic; supports redundant tunnels.
ExpressRoute Failover: VPN gateway provides a backup path if ExpressRoute fails.
Zone-redundant Gateways: Deploy gateways across availability zones for resilience against zone failures (requires specific SKUs and Standard IPs).

**Azure ExpressRoute** is a private, dedicated connection between your on-premises infrastructure and Microsoft cloud services (e.g., Azure, Microsoft 365). It bypasses the public internet, providing higher reliability, faster speeds, consistent latency, and better security.
**Key Features and Benefits:**
Private Connectivity: Traffic doesn’t travel over the public internet.
High Performance: More reliable and secure with lower latency.
Access to Microsoft Services: Supports Azure, Microsoft 365, Dynamics 365, etc.
Built-in Redundancy: Redundant devices in each peering location ensure high availability.
Dynamic Routing: Uses BGP for exchanging routes between your network and Azure.
Global Connectivity:
Within regions via geopolitical boundaries.
Across regions using ExpressRoute Global Reach to connect different sites (e.g., Asia to Europe).
Connectivity Models:
CloudExchange Colocation: Virtual cross-connect from a colocation facility.
Point-to-Point Ethernet: Direct Ethernet connection between your site and Azure.
Any-to-Any (IP VPN): Integrates your WAN with Azure, like connecting branch offices.
ExpressRoute Direct: Connect directly at Microsoft peering locations with up to 100 Gbps capacity.
Security Considerations:
Data travels over a private circuit, not the internet.
Some services (e.g., DNS, CDN, certificate checks) still use the public internet.
In short: Azure ExpressRoute enables private, high-speed, and secure connectivity between your on-premises environment and Microsoft cloud services, with multiple connection options and built-in redundancy.

**Azure DNS** is a hosting service for Domain Name System (DNS) domains, enabling name resolution using Microsoft Azure's global infrastructure. It allows you to manage DNS records with the same tools and credentials used across your Azure services.
**Key Benefits:**
Reliability & Performance
Hosted on Azure’s global network of DNS name servers.
Uses anycast networking for fast response times and high availability.
Security
Built on Azure Resource Manager, offering:
Role-Based Access Control (RBAC)
Activity logs
Resource locks to prevent accidental changes
Ease of Use
Integrated with the Azure portal, PowerShell, Azure CLI, REST API, and SDKs.
Unified billing and support with other Azure services.
Private DNS for Virtual Networks
Supports private DNS zones, allowing use of custom domain names within Azure virtual networks.
Alias Records
Lets you point DNS records directly to Azure resources (e.g., public IPs, Traffic Manager, CDN).
Automatically updates if the underlying resource’s IP changes.

**LRS- 11 9s of durability**
<img width="218" height="226" alt="image" src="https://github.com/user-attachments/assets/5de5d3dc-74f9-4e03-8775-f358061a4ed0" />

**ZRS - 12 9s of durability**
<img width="395" height="385" alt="image" src="https://github.com/user-attachments/assets/092e1055-327f-4c9b-93ef-c838c45f95c0" />

**GRS - 16 9s**
<img width="568" height="290" alt="image" src="https://github.com/user-attachments/assets/7c8ef05c-67bb-4801-9e01-d8d4d6e29e1c" />

**GZRS - 16 9s**
<img width="688" height="418" alt="image" src="https://github.com/user-attachments/assets/793ae29a-7479-4a57-baf4-07fb18106eeb" />

**Azure File Movement Options**
Azure provides several tools to help move and manage files of all sizes—from large migrations to individual file transfers. Here are the key options for smaller-scale file movement:
**1. AzCopy**
Type: Command-line tool
Use cases: Upload, download, or copy files/blobs to/from Azure Storage
Features:
Supports file movement between storage accounts
One-way sync (source to destination only)
Works with other cloud providers
Limitation: Not bi-directional; no automatic syncing based on timestamps or metadata
**2. Azure Storage Explorer**
Type: Graphical desktop application (Windows, macOS, Linux)
Use cases: Visual file/blobs management
Features:
Upload, download, move files between storage accounts
Uses AzCopy behind the scenes
User-friendly GUI for managing Azure Storage
**3. Azure File Sync**
Type: Sync service for Windows file servers
Use cases: Centralize and sync on-prem file shares with Azure Files
Features:
Bi-directional sync between Azure and on-premises
Supports SMB, NFS, FTPS protocols locally
Enables cloud tiering (frequently used files local, others in cloud)
Supports multiple caches globally
Allows quick recovery from server failure by reinstalling on a new server


<img width="676" height="220" alt="image" src="https://github.com/user-attachments/assets/6a297e56-e73a-4ec3-90d1-dc1e89551ca9" />









