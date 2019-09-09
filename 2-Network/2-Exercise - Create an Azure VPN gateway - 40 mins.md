# Exercise - Create an Azure VPN gateway

* 40 minutes

You want to ensure that you can connect clients or sites within your environment into Azure using encrypted tunnels across the public Internet. In this lab, you'll create a point-to-site VPN gateway, and then connect to that gateway from your client computer. You'll use native Azure certificate authentication connections for security.

You will carry out the following process:

1. Create a RouteBased VPN gateway.

2. Upload the public key for a root certificate for authentication purposes.

3. Generate a client certificate from the root certificate, and then install the client certificate on each client computer that will connect to the virtual network for authentication purposes.

4. Create VPN client configuration files, which contain the necessary information for the client to connect to the virtual network.

## Setup

To complete this module, you will use Azure PowerShell from your local Windows 10 computer.

We'll start by setting up variables to be used when we create a virtual network. Open a new PowerShell session and create the following variables:

**PowerShell**

    $VNetName  = "VNetData"
    $FESubName = "FrontEnd"
    $BESubName = "Backend"
    $GWSubName = "GatewaySubnet"
    $VNetPrefix1 = "192.168.0.0/16"
    $VNetPrefix2 = "10.254.0.0/16"
    $FESubPrefix = "192.168.1.0/24"
    $BESubPrefix = "10.254.1.0/24"
    $GWSubPrefix = "192.168.200.0/26"
    $VPNClientAddressPool = "172.16.201.0/24"
    $ResourceGroup = "VpnGatewayDemo"
    $Location = "East US"
    $GWName = "VNetDataGW"
    $GWIPName = "VNetDataGWPIP"
    $GWIPconfName = "gwipconf"

## Configure a virtual network

1. Create a resource group.

   **PowerShell**

        New-AzResourceGroup -Name $ResourceGroup -Location $Location

2. Create subnet configurations for the virtual network. These have the name **FrontEnd, BackEnd**, and **GatewaySubnet**. All of these subnets exist within the virtual network prefix.

    **PowerShell**

        $fesub = New-AzVirtualNetworkSubnetConfig -Name $FESubName -AddressPrefix $FESubPrefix
        $besub = New-AzVirtualNetworkSubnetConfig -Name $BESubName -AddressPrefix $BESubPrefix
        $gwsub = New-AzVirtualNetworkSubnetConfig -Name $GWSubName -AddressPrefix $GWSubPrefix

3. Next, create the virtual network using the subnet values and a static DNS server.

    **PowerShell**

        New-AzVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroup -Location $Location -AddressPrefix $VNetPrefix1,$VNetPrefix2 -Subnet $fesub, $besub, $gwsub -DnsServer 10.2.1.3

4. Now specify the variables for this network that you have just created.

    **PowerShell**

        $vnet = Get-AzVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroup
        $subnet = Get-AzVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet

5. Request a dynamically assigned public IP address.

    **PowerShell**

        $pip = New-AzPublicIpAddress -Name $GWIPName -ResourceGroupName $ResourceGroup -Location $Location -AllocationMethod Dynamic
        $ipconf = New-AzVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip

## Create the VPN gateway

When creating this VPN gateway:

* GatewayType must be Vpn
* VpnType must be RouteBased

**Note:**
Part of the exercise can take up to 45 minutes to complete.

1. To create the VPN gateway, run the following command and press Enter.

    **PowerShell**

        New-AzVirtualNetworkGateway -Name $GWName -ResourceGroupName $ResourceGroup `
          -Location $Location -IpConfigurations $ipconf -GatewayType Vpn `
          -VpnType RouteBased -EnableBgp $false -GatewaySku VpnGw1 -VpnClientProtocol "IKEv2"

2. Wait for the command output to appear.

## Add the VPN client address pool

1. Run the following command and press Enter.

    **PowerShell**

        $Gateway = Get-AzVirtualNetworkGateway -ResourceGroupName $ResourceGroup -Name $GWName
        Set-AzVirtualNetworkGateway -VirtualNetworkGateway $Gateway -VpnClientAddressPool $VPNClientAddressPool

2. Wait for the command output to appear.

## Generate a client certificate

With the network infrastructure created on Azure, we need to create a self-signed client certificate on our local machine. This can be done similarly on most operating systems, but we will cover how to generate your client certificate on Windows 10 using PowerShell with the Azure PowerShell module and the Windows **Certificate Manager** utility.

1. Our first step is to create the self-signed root certificate. Run the following command.

    **PowerShell**

        $cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature `
        -Subject "CN=P2SRootCert" -KeyExportPolicy Exportable `
        -HashAlgorithm sha256 -KeyLength 2048 `
        -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign

2. Next, generate a client certificate signed by your new root certificate.

    **PowerShell**

        New-SelfSignedCertificate -Type Custom -DnsName P2SChildCert -KeySpec Signature `
        -Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
        -HashAlgorithm sha256 -KeyLength 2048 `
        -CertStoreLocation "Cert:\CurrentUser\My" `
        -Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")

With our certificates generated, we need to export our root certificate's public key.

1. Run `certmgr` from PowerShell to open the Certificate Manager.

2. Navigate to **Personal** > **Certificates**. Find and right-click the **P2SRootCert** certificate in the list and select **All tasks** > **Export...**.

3. In the Certificate Export Wizard, click **Next**.

4. Ensure that **No, do not export the private key** is selected, and then click **Next**.

5. On the **Export File Format** page, ensure that **Base-64 encoded X.509 (.CER)** is selected, and then click **Next**.

6. In the **File to Export** page, under **File name**, navigate to a location you'll remember and save the file as **P2SRootCert.cer**, and then click Next.

7. On the **Completing the Certificate Export Wizard** page, click **Finish**.

8. On the **Certificate Export Wizard** message box, click **OK**.

## Upload the root certificate public key information

1. In the PowerShell window, execute the following command to declare a variable for the certificate name:

    **PowerShell**

        $P2SRootCertName = "P2SRootCert.cer"

2. Replace the `<cert-path>` placeholder with the export location of your root certificate and execute the following command:

    **PowerShell**

        $filePathForCert = "<cert-path>\P2SRootCert.cer"
        $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
        $CertBase64 = [system.convert]::ToBase64String($cert.RawData)
        $p2srootcert = New-AzVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64

3. With the group name set, upload the certificate to Azure with the following command.

    **PowerShell**

        Add-AzVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname $GWName -ResourceGroupName $ResourceGroup -PublicCertData $CertBase64

    Azure will now recognize this certificate as a trusted root certificate for our virtual network.

## Configure the native VPN client

1. Execute the following command to create VPN client configuration files in .ZIP format.

    **PowerShell**

        $profile = New-AzVpnClientConfiguration -ResourceGroupName $ResourceGroup -Name $GWName -AuthenticationMethod "EapTls"
        $profile.VPNProfileSASUrl

2. Copy the URL returned in the output from this command and paste it into your browser. Your browser should start downloading a .ZIP file. Extract the archive contents and put them in a suitable location.

    **Note**

    Some browsers will initially attempt to block downloading this ZIP file as a dangerous download. You will need to override this in your browser to be able to extract the archive contents.

3. In the extracted folder, navigate to either the **WindowsAmd64** folder (for 64-bit Windows computers) or the **WindowsX86** folder (for 32-bit computers).

    **Note**

    If you want to configure a VPN on a non-Windows machine, you can use the certificate and settings files from the **Generic** folder.

4. Double-click on the **VpnClientSetup{architecture}.exe** file, with `{architecture}` reflecting your architecture.

5. In the **Windows protected your PC** screen, click **More info**, and then click **Run anyway**.

6. In the **User Account Control** dialog box, click **Yes**.

7. In the **VNetData** dialog box, click **Yes**.

## Connect to Azure

1. Press the Windows key, type **Settings** and press Enter.

2. In the **Settings** window, click **Network and Internet**.

3. In the left-hand pane, click **VPN**.

4. In the right-hand pane, click **VNetData**, and then click **Connect**.

5. In the VNetData window, click **Connect**.

6. In the next VNetData window, click **Continue**.

7. In the **User Account Control** message box, click **Yes**.

    **Note**

    If these steps do not work, you may need to restart your computer.

## Verify your connection

1. In a new Windows command prompt, run `IPCONFIG /ALL`.

2. Copy the IP address under PPP adapter VNetData, or write it down.

3. Confirm that IP address is in the **VPNClientAddressPool range of 172.16.201.0/24**.

4. You have successfully made a connection to the Azure VPN gateway.

You just set up a VPN gateway, allowing you to make an encrypted client connection to a virtual network in Azure. This approach is great with client computers and smaller site-to-site connections.
