
# Create a P2S User VPN connection using Azure Virtual WAN - Azure AD authentication

This article shows you how to use Virtual WAN to connect to your resources in Azure. In this article, you create a point-to-site User VPN connection to Virtual WAN that uses Azure Active Directory (Azure AD) authentication. Azure AD authentication is only available for gateways that use the OpenVPN protocol.

[!INCLUDE [OpenVPN note](../../includes/vpn-gateway-openvpn-auth-include.md)]

In this article, you learn how to:

* Create a virtual WAN
* Create a User VPN configuration
* Download a virtual WAN User VPN profile
* Create a virtual hub
* Edit a hub to add P2S gateway
* Connect a VNet to a virtual hub
* Download and apply the User VPN client configuration
* View your virtual WAN

:::image type="content" source="./media/virtual-wan-about/virtualwanp2s.png" alt-text="Virtual WAN diagram.":::

## Before you begin

Verify that you've met the following criteria before beginning your configuration:

* You have a virtual network that you want to connect to. Verify that none of the subnets of your on-premises networks overlap with the virtual networks that you want to connect to. To create a virtual network in the Azure portal, see the [Quickstart](../virtual-network/quick-create-portal.md).

* Your virtual network doesn't have any virtual network gateways. If your virtual network has a gateway (either VPN or ExpressRoute), you must remove all gateways. This configuration requires that virtual networks are connected instead, to the Virtual WAN hub gateway.

* Obtain an IP address range for your hub region. The hub is a virtual network that is created and used by Virtual WAN. The address range that you specify for the hub can't overlap with any of your existing virtual networks that you connect to. It also can't overlap with your address ranges that you connect to on premises. If you're unfamiliar with the IP address ranges located in your on-premises network configuration, coordinate with someone who can provide those details for you.

* If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

## <a name="wan"></a>Create a virtual WAN

From a browser, navigate to the [Azure portal](https://portal.azure.com) and sign in with your Azure account.

[!INCLUDE [Create a virtual WAN](../../includes/virtual-wan-create-vwan-include.md)]

## <a name="user-config"></a>Create a User VPN configuration

A User VPN configuration defines the parameters for connecting remote clients. It's important to create the User VPN configuration before configuring your virtual hub with P2S settings, as you must specify the User VPN configuration you want to use.

1. Navigate to your **Virtual WAN ->User VPN configurations** page and click **+Create user VPN config**.


1. On the **Basics** page, specify the parameters.



    * **Configuration name** - Enter the name you want to call your User VPN Configuration.
    * **Tunnel type** - Select OpenVPN from the dropdown menu.

1. Click **Azure Active Directory** to open the page.


    Toggle **Azure Active Directory** to **Yes** and supply the following values based on your tenant details. You can view the necessary values on the Azure Active Directory page for Enterprise applications in the portal.
   * **Authentication method** - Select Azure Active Directory.
   * **Audience** - Type in the Application ID of the [Azure VPN](openvpn-azure-ad-tenant.md) Enterprise Application registered in your Azure AD tenant.
   * **Issuer** - `https://sts.windows.net/<your Directory ID>/`
   * **AAD Tenant:** TenantID for the Azure AD tenant. Make sure there is no `/` at the end of the AAD tenant URL. 

     * Enter `https://login.microsoftonline.com/{AzureAD TenantID}` for Azure Public AD
     * Enter `https://login.microsoftonline.us/{AzureAD TenantID}` for Azure Government AD
     * Enter `https://login-us.microsoftonline.de/{AzureAD TenantID}` for Azure Germany AD
     * Enter `https://login.chinacloudapi.cn/{AzureAD TenantID}` for China 21Vianet AD

1. Click **Create** to create the User VPN configuration. You'll select this configuration later in the exercise.

## <a name="site"></a>Create an empty hub

For this exercise, we create an empty virtual hub in this step and, in the next section, you add a P2S gateway to this hub. However, you can combine these steps and create the hub with the P2S gateway settings all at once. The result is the same either way. After configuring the settings, click **Review + create** to validate, then **Create**.

[!INCLUDE [Create an empty hub](../../includes/virtual-wan-hub-basics.md)]

## <a name="hub"></a>Add a P2S gateway to a hub

This section shows you how to add a gateway to an already existing virtual hub. This step can take up to 30 minutes for the hub to complete updating. 

1. Navigate to the **Hubs** page under the virtual WAN.
1. Click the name of the hub that you want to edit to open the page for the hub.
1. Click **Edit virtual hub** at the top of the page to open the **Edit virtual hub** page.
1. On the **Edit virtual hub** page, check the checkboxes for **Include vpn gateway for vpn sites** and **Include point-to-site gateway** to reveal the settings. Then configure the values.


   * **Gateway scale units**: Select the Gateway scale units. Scale units represent the aggregate capacity of the User VPN gateway. If you select 40 or more gateway scale units, plan your client address pool accordingly. For information about how this setting impacts the client address pool, see [About client address pools](about-client-address-pools.md). For information about gateway scale units, see the [FAQ](virtual-wan-faq.md#for-user-vpn-point-to-site--how-many-clients-are-supported).
   * **User VPN configuration**: Select the configuration that you created earlier.
   * **User Groups to Address Pools Mapping**: For information about this setting, see [Configure user groups and IP address pools for P2S User VPNs (preview)](user-groups-create.md).

1. After configuring the settings, click **Confirm** to update the hub. It can take up to 30 minutes to update a hub.

## <a name="connect-vnet"></a>Connect VNet to hub

In this section, you create a connection between your virtual hub and your VNet.

[!INCLUDE [Connect virtual network](../../includes/virtual-wan-connect-vnet-hub-include.md)]

## <a name="download-profile"></a>Download User VPN profile

All of the necessary configuration settings for the VPN clients are contained in a VPN client configuration zip file. The settings in the zip file help you easily configure the VPN clients. The VPN client configuration files that you generate are specific to the User VPN configuration for your gateway. You can download global (WAN-level) profiles, or a profile for a specific hub. For information and additional instructions, see [Download global and hub profiles](global-hub-profile.md). The following steps walk you through downloading a global WAN-level profile.

[!INCLUDE [Download profile](../../includes/virtual-wan-p2s-download-profile-include.md)]

##  <a name="configure-client"></a>Configure User VPN clients

Each computer that connects must have a client installed. You configure each client by using the VPN User client profile files that you downloaded in the previous steps. Use the article that pertains to the operating system that you want to connect.

### To configure macOS VPN clients (Preview)

For **macOS** client instructions, see [Configure a VPN client - macOS (Preview)](openvpn-azure-ad-client-mac.md).

### To configure Windows VPN clients

[!INCLUDE [Download Azure VPN client](../../includes/vpn-gateway-download-vpn-client.md)]

#### <a name="import"></a>To import a VPN client profile (Windows)

Sure! Here's a step-by-step procedure to connect and import a VPN client profile from an Azure VPN client:

1. **Install Azure VPN Client:**
   If you haven't already installed the Azure VPN client on your computer, you can download and install it from the official Microsoft website.

2. **Launch Azure VPN Client:**
   After the installation is complete, launch the Azure VPN client on your computer. It should be available in your list of applications or system tray.

3. **Sign in to Azure:**
   Sign in to your Azure account using your credentials. Make sure you have the necessary permissions to access VPN resources in your Azure subscription.

4. **Navigate to VPN Gateway:**
   In the Azure VPN client, navigate to the "VPN Gateway" section. Here, you'll find a list of VPN gateways associated with your Azure account.

5. **Select the VPN Gateway:**
   Choose the VPN gateway that you want to connect to and import the profile for. You may have multiple VPN gateways if you have set up several VPN connections in Azure.

6. **Download the VPN Client Profile:**
   Once you have selected the VPN gateway, look for an option to download the VPN client profile. This profile will contain the necessary configuration information for your VPN connection.

7. **Save the Profile to a Local Location:**
   Save the downloaded VPN client profile to a location on your local computer where you can easily access it.

8. **Import the VPN Client Profile:**
   In the Azure VPN client, there should be an option to import a VPN client profile. Click on it and browse to the location where you saved the downloaded profile. Select the profile and import it into the Azure VPN client.

9. **Configure VPN Connection Settings (if needed):**
   Depending on your network setup and requirements, you might need to configure some additional VPN connection settings. These settings might include authentication methods, encryption, or proxy configurations. Consult your network administrator or the Azure documentation for specific requirements.

   Sure! I've added the step to include the specified routes in the VPN client profile configuration:

```markdown
# Connect and Import VPN Client Profile from Azure VPN Client

1. **Open the VPN Client Profile:**
   Use a text editor to open the downloaded VPN client profile.

2. **Add the Route Configuration:**
   Find the `<clientconfig>` section in the VPN client profile. Within the `<includeroutes>` tag, add the following routes:

   ```xml
    <route>
      <destination>0.0.0.0</destination>
      <mask>1</mask>
    </route>
    <route>
      <destination>128.0.0.0</destination>
      <mask>1</mask>
    </route>
   ```

   These routes will include all traffic to the VPN client ( VPN Client to Azure Firewall ).

10. **Save the Changes:**
    After adding the route configuration, save the changes to the VPN client profile.

11. **Import the Updated VPN Client Profile:**
    In the Azure VPN client, there should be an option to import a VPN client profile. Click on it and browse to the location where you saved the updated profile. Select the profile and import it into the Azure VPN client.

12. **Configure VPN Connection Settings (if needed):**
    Depending on your network setup and requirements, you might need to configure some additional VPN connection settings. These settings might include authentication methods, encryption, or proxy configurations. Consult your network administrator or the Azure documentation for specific requirements.

13. **Connect to the VPN:**
    After successfully importing the VPN client profile and configuring any necessary settings, you should be ready to connect to the VPN. Click on the "Connect" or "Start" button in the Azure VPN client to initiate the connection.

14. **Enter Credentials (if prompted):**
    If your VPN connection requires authentication, enter the necessary credentials (username and password) when prompted.

15. **Connected!**
    Once the VPN connection is established, you should see a confirmation message in the Azure VPN client indicating that you are connected to the VPN gateway.

That's it! You have successfully connected to the VPN using the Azure VPN client, and the specified routes have been included in the VPN client profile configuration. Now you can securely access resources in your Azure virtual network and any other connected networks.
```
