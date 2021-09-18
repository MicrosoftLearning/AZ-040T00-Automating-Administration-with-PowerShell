---
lab:
    title: 'Lab: Azure resource management with PowerShell'
    module: 'Module 9: Managing Azure resources with PowerShell'
---

# Lab: Azure resource management with PowerShell

## Scenario

You're a system administrator for the London branch office of Adatum Corporation. You need to evaluate the Microsoft Azure platform to run virtual machines (VMs) and other resources for your company. As part of your evaluation, you also want to test PowerShell administration of Azure-based resources.

# Objectives

After completing this lab, you'll be able to:

- Install the Az module for Windows PowerShell.
- Run and use the Azure Cloud Shell environment.
- Manage Azure VMs and disks by using PowerShell.

## Estimated time: 60 minutes

## Lab setup

Virtual machines: **LON-DC1** and **LON-CL1**

Username: **Adatum\\Administrator**

Password: **Pa55w.rd**

For this lab, you'll use the available virtual machine environment. Before you begin the lab, complete the following steps:

1. Open **LON-DC1** and sign in as **Adatum\\Administrator** with the password **Pa55w.rd**.
1. Repeat step 1 for **LON-CL1**.

## Exercise 1: Activating the Azure subscription and installing the PowerShell Az module

### Scenario 1

You need to make sure that you activate your trial Azure subscription and install the Az module for Windows PowerShell.

The main tasks for this exercise are:

1. Activate your Azure subscription by using the Azure pass voucher.
1. Install the Azure Az module for PowerShell.

### Task 1: Activate your Azure subscription by using Azure pass voucher

1. On **LON-CL1**, open the Microsoft Edge browser and navigate to **https://www.microsoftazurepass.com/**.
1. Sign in with the Microsoft account that you want to use for your trial Azure subscription.
1. Use the Azure pass code provided by your instructor or lab hosting provider.
1. Ensure that the **Subscriptions** page displays **Azure Pass - Sponsorship** with an **Active** status and that you have a balance of 50 USD.

### Task 2: Install the Azure Az module for PowerShell

1. On **LON-CL1**, start the PowerShell 7.1 environment.
1. Check your version of PowerShell by using `$PSVersionTable.PSVersion`.
1. Set the execution policy to **RemoteSigned** for the current user.
1. From the PowerShell Gallery, install the Az module for the current user by using the **Install-Module** command.
1. Use **Connect-AzAccount** to sign in to your Azure subscription.

## Exercise 2: Using Azure Cloud Shell

### Scenario 2

To work with other Azure resources such as Azure VMs, you need to create an Azure resource group. You decide to use Azure Cloud Shell to perform this task.

The main task for this exercise is:

- Use Azure Cloud Shell to create a resource group.

### Task 1: Use Azure Cloud Shell to create a resource group

1. Check your Azure tenant in the Azure portal to ensure that no Azure VMs or storage accounts exist.
1. Start the Azure Cloud Shell environment.
1. Check your subscription by using the **Get-AzSubscription** command.
1. Use the **Get-AzResourceGroup** command to verify that no resource groups exist.
1. Switch to the **Bash** environment in Azure Cloud Shell and then use **az account list** and **az resource list** to check subscriptions and resource groups. Switch back to the PowerShell environment in Azure Cloud Shell.
1. Use the **New-AzResourceGroup** command to create a new resource group in the West Europe region. Name the resource group *YourNameM9*, and replace *YourName* with your first name.

## Exercise 3: Managing Azure resources with Azure PowerShell

After you create the Azure subscription and resource group, you want to use PowerShell to create an Azure VM based on a Windows Server 2016 image.

The main tasks for this exercise are as follows:

1. Create an Azure VM by using PowerShell.
1. Add a disk to Azure VM by using PowerShell.

### Task 1: Create an Azure VM by using PowerShell

1. In the PowerShell 7.1 window, use the **Get-Credential** command to store admin credentials for the new Azure VM in the `$cred` variable. Do not use name Admin for administrator.
1. In the PowerShell 7.1 window, use the following command to define the VM parameters (replace *yourname* with your real name):

   ```powershell
   $vmParams = @{
     ResourceGroupName = 'yournameM9'
     Name = 'TestVM1'
     Location = 'westeurope'
     ImageName = 'Win2016Datacenter'
     PublicIpAddressName = 'TestPublicIp'
     Credential = $cred
     OpenPorts = 3389
   }
   ```

1. Use the **New-AzVM** command to create a new VM with the parameters defined in the previous step. Store this in the `$NewVM1` variable.
1. To check the parameters on the new VM, enter the following commands, and then select Enter:

   ```powershell
   $NewVM1
   $newVM1.OSProfile | Select-Object ComputerName,AdminUserName
   $newVM1 | Get-AzNetworkInterface | Select-Object -ExpandProperty IpConfigurations | Select-Object Name,PrivateIpAddress
   ```

1. To find the public IP address on the Azure VM you created so you can connect to it, enter the following commands, and then select Enter:

   ```powershell
   $publicIp = Get-AzPublicIpAddress -Name TestPublicIp -ResourceGroupName yournameM9
   
   $publicIp | Select-Object Name,IpAddress,@{label='FQDN';expression={$_.DnsSettings.Fqdn}}
   ```

1. Note the value of IPAddress in the table output.
1. Use the **mstsc.exe** tool to connect to the Azure VM you created. Sign in with the credentials that you defined in the first step.

### Task 2: Add a disk to the Azure VM by using PowerShell

1. Use the Azure portal to navigate to the properties for **TestVM1**.
1. Ensure that **TestVM1** has only operating system disk installed.
1. Create a data disk for the existing VM by using the following commands and selecting Enter after each:

   ```powershell
   $VirtualMachine = Get-AzVM -ResourceGroupName "yournameM9" -Name "TestVM1"
   Add-AzVMDataDisk -VM $VirtualMachine -Name "disk1" -LUN 0 -Caching ReadOnly -DiskSizeinGB 1 -CreateOption Empty
   Update-AzVM -ResourceGroupName "yournameM9" -VM $VirtualMachine
   ```

1. Switch to the Azure portal and refresh the **Disks** page. Ensure that there's a new disk called **disk1** in the **Data disks** section.
