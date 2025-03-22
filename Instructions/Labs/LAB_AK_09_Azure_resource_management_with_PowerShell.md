---
lab:
    title: 'Lab: Azure resource management with PowerShell'
    type: 'Answer Key'
    module: 'Module 9: Managing Azure resources with PowerShell'
---

# Azure resource management with PowerShell

## Exercise 1: Activating the Azure subscription and installing the PowerShell Az module

#### Task 1: Open the Azure portal

1. On the taskbar, select the **Microsoft Edge** icon.

1. In the browser window, browse to the Azure portal at `https://portal.azure.com`, and then sign in with the account you'll be using for this lab.

   > **Note**: If this is your first time signing in to the Azure portal, you'll be offered a tour of the portal. If you prefer to skip the tour, select **Maybe later** to begin using the portal.

### Task 2: Install the Azure Az module for PowerShell

1. Select the **Start** menu, and then enter **pwsh**.

1. In the results list, right-click **PowerShell 7 (x64)** or activate its context menu, and select **Run as administrator**.

1. In the **Administrator: PowerShell 7 (x64)** window, enter the following command, and then press the Enter key to check your PowerShell version:

   ```powershell
   $PSVersionTable.PSVersion
   ```

1. Enter the following commands, and then press the Enter key to update the PowerShell 7:
      
   ```powershell
   # Update PowerShell 7 to the latest version
   iex "& { $(irm https://aka.ms/install-powershell.ps1 -UseBasicP) }"

   # Open a new PowerShell 7 window as an administrator
   Start-Process -FilePath "C:\Users\Administrator.ADATUM\AppData\Local\Microsoft\powershell\pwsh.exe" -Verb RunAs

   # Close the current PowerShell window
   Stop-Process -Id $PID 
   
   ```  

1. To set your execution policy to the proper value so you can install the Az module, enter the following command, and then press the Enter key. Enter **Y** to confirm your choice:

   ```powershell
   Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
   ```

1. To install the Az module, enter the following command. Enter **Y** to confirm your choice:

   ```powershell
   Install-Module -Name Az -Scope CurrentUser -Repository PSGallery -Force
   ```

1. Wait until the module is installed and the command prompt displays.

1. After the Az module is installed, enter the following command:

   ```powershell
   Connect-AzAccount
   ```

1. When prompted, sign in with the account that you used in the previous task to provision your Azure subscription.

1. Verify that after sign-in, your account name and the Azure subscription details are listed.

## Exercise 2: Using Azure Cloud Shell

### Task 1: Use Azure Cloud Shell to create a resource group

1. On the **LON-CL1** computer, switch to the web browser window displaying the Azure portal.

1. On the Microsoft Azure portal homepage, select **Virtual Machines**. Ensure that no virtual machines (VMs) are created. Select **Home**.

1. On the Microsoft Azure portal homepage, select **Storage accounts**. Ensure that no storage accounts are created. Select **Home**.

1. On the Microsoft Azure portal homepage, select the **Cloud Shell** icon.

1. In the **Welcome to Azure Cloud Shell** window, select **PowerShell**.

1. On the **You have no storage mounted** page, review the note about the missing storage account that's needed for Cloud Shell to run. Verify that in the **Subscription** field, your subscription is selected, and then select **Create storage**. Wait until the storage account is created.

1. When your storage account is created, the **Cloud Shell** console should open, and you should get a prompt in the format **PS /home/yourname>**.

1. At the PowerShell prompt, enter `Get-AzSubscription`, and then press the Enter key to review your subscriptions.

1. Enter `Get-AzResourceGroup` to review the resource group information.

1. Use the drop-down list to switch from PowerShell to the **Bash** shell and confirm your choice.

1. At the Bash shell prompt, enter `az account list`, and then press the Enter key to review the information about your subscription. Also, try tab completion.

1. Enter `az resource list` to review the resource group information.

1. Switch back to the PowerShell interface.

1. In the **PowerShell** console, enter the following command, and then press the Enter key to create a new resource group (replace the `<resource-group-name>` placeholder with your first name):

    ```powershell
    New-AzResourceGroup -Name <resource-group-name> -Location westeurope
    ```

1. Verify that your new resource group is created. Record the name of your resource group. You will need it in the next exercise of this lab.

## Exercise 3: Managing Azure resources with Azure PowerShell

### Task 1: Create an Azure VM by using PowerShell

1. In the PowerShell window, enter the following command to provide the admin credentials for the operating system of the Azure VM you will create in this exercise:

   ```powershell
   $cred = Get-Credential -Message "Enter an admin username and password for the operating system"
   ```

1. When prompted, enter an arbitrary username and password that you want to use as admin credentials for the new VM. Do not use **Admin** or **Administrator** as the username. Choose a complex, at least 8 character-long password that includes lower case letters, upper case letters, digits, and at least one special character.

1. In the PowerShell window, enter the following command to define the VM parameters, and then press the Enter key (replace the `<resource-group-name>` placeholder with the name of the resource group you created in the previous exercise):

   ```powershell
   $vmParams = @{
     ResourceGroupName = '<resource-group-name>'
     Name = 'TestVM1'
     Location = 'westeurope'
     ImageName = 'Win2019Datacenter'
     PublicIpAddressName = 'TestPublicIp'
     Credential = $cred
     OpenPorts = 3389
   }
   ```

1. To create a new VM based on these parameters and store the reference to it in the `newVM1` variable, enter the following command, and then press the Enter key:

   ```powershell
   $newVM1 = New-AzVM @vmParams
   ```

   >**Note:** Wait until the Azure VM is created.

1. To identify the configuration settings of the new VM, enter the following commands, and then press the Enter key after each:

   ```powershell
   $NewVM1

   $newVM1.OSProfile | Select-Object ComputerName,AdminUserName

   $newVM1 | Get-AzNetworkInterface | Select-Object -ExpandProperty IpConfigurations | Select-Object Name,PrivateIpAddress
   ```

1. To retrieve the name of the resource group into which you deployed the Azure VM and store it in a variable, enter the following command, and then press the Enter key:

   ```powershell
   $rgName = $NewVM1.ResourceGroupName
   ```

1. To identify the public IP address assigned to the network interface of the Azure VM so you can connect to it, enter the following commands, and then press the Enter key:

   ```powershell
   $publicIp = Get-AzPublicIpAddress -Name TestPublicIp -ResourceGroupName $rgName
   
   $publicIp | Select-Object Name,IpAddress,@{label='FQDN';expression={$_.DnsSettings.Fqdn}}
   ```

1. Note the value of **IPAddress** in the table output.

1. Enter the following command, and then press the Enter key to connect to the VM by using Remote Desktop:

   ```powershell
   mstsc.exe /v $publicIp.IpAddress
   ```

1. When prompted, sign in with the admin credentials you provided during the Azure VM provisioning. Ensure that you're connected to the Windows Server 2019 VM and then shut down the operating system. This will automatically terminate your Remote Desktop session.

### Task 2: Add a disk to the Azure VM by using PowerShell

1. On the **LON-CL1** computer, switch to the web browser window displaying the Azure portal and navigate to the **Virtual Machines** page.

1. On the **Virtual Machines** page, select the **TestVM1** entry.

1. On the **Overview** page of the **TestVM1** VM, review its parameters and, in the navigation menu, in the **Settings** section, select **Disks**. 

1. Review the list of disks and verify that only a single disk is listed (OS disk).

1. To create a data disk for the existing VM, in the PowerShell window, enter the following commands, and press the Enter key after each:

   ```powershell
   $VirtualMachine = Get-AzVM -ResourceGroupName "<resource-group-name>" -Name "TestVM1"

   Add-AzVMDataDisk -VM $VirtualMachine -Name "disk1" -LUN 0 -Caching ReadOnly -DiskSizeinGB 1 -CreateOption Empty

   Update-AzVM -ResourceGroupName "<resource-group-name>" -VM $VirtualMachine
   ```

1. Switch to the Azure portal and refresh the **TestVM1 \| Disks** page. Verify that the listing of disks includes a new disk called **disk1** in the **Data disks** section.

### Task 3: Delete the Azure resources

1. On the **LON-CL1** computer, switch back to the **PowerShell** window.

1. In the **PowerShell** console, enter the following command, and then press the Enter key to delete the resource group and all of its resources, which you created earlier in this lab:

    ```powershell
    Remove-AzResourceGroup -Name $rgName -Force
    ```

1. Wait for the command to complete. This should take less than 5 minutes.
