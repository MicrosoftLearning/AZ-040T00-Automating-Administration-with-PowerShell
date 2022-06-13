---
lab:
    title: 'Lab: Using PSProviders and PSDrives with PowerShell'
    type: 'Answer Key'
    module: 'Module 4: Using PSProviders and PSDrives'
---

# Lab answer key: Using PSProviders and PSDrives with PowerShell

## Exercise 1: Creating files and folders on a remote computer

### Task 1: Create a new folder on a remote computer

1. On **LON-CL1**, select **Start**, and then enter **powersh**.
1. From the results list, right-click **Windows PowerShell** or activate its context menu, and then select **Run as administrator**.
1. To review help for the **New-Item** cmdlet in a separate window, in the **Administrator: Windows PowerShell** console, enter the following command, and then press the Enter key:

   ```powershell
   Get-Help New-Item –ShowWindow
   ```

1. In the output from **Get-Help**, notice the *–Name* and *–ItemType* parameters, then review the example commands, and close the **New-Item Help** window.
1. To create a new **ScriptShare** folder in **\\\\Lon-Svr1\\C$\\**, in the console, enter the following command, and then press the Enter key:

   ```powershell
   New-Item –Path \\Lon-Svr1\C$\ –Name ScriptShare –ItemType Directory
   ```

### Task 2: Create a new PSDrive mapping to the remote file folder

1. To display the help for the **New-PSDrive** cmdlet, enter the following command, and then press the Enter key:

   ```powershell
   Get-Help New-PSDrive –ShowWindow
   ```

1. Review the following information, and then close the **New-PSDrive Help** window:
    - Help information
    - *–Name*, *–Root*, and *–PSProvider* parameters
    - Example commands

1. To create a new PSDrive mapping, enter the following command, and then press the Enter key:

   ```powershell
   New-PSDrive –Name ScriptShare –Root \\Lon-Svr1\c$\ScriptShare –PSProvider FileSystem
   ```

### Task 3: Create a file on the mapped drive

1. To review help for the **Set-Location** cmdlet, enter the following command, and then press the Enter key:

   ```powershell
   Get-Help Set-Location –ShowWindow
   ```

1. Review the help information, and then close the **Set-Location Help** window.
1. To change to the ScriptShare: location, enter the following command, and then press the Enter key:

   ```powershell
   Set-Location ScriptShare:
   ```

1. To create a new file, enter the following command, and then press the Enter key:

   ```powershell
   New-Item script.txt
   ```

1. To review a directory listing, enter the following command, and then press the Enter key:

   ```powershell
   Get-ChildItem
   ```

1. Verify that the **script.txt** file is listed.

## Exercise 2: Creating a registry key for your future scripts

### Task 1: Create the registry key to store script configurations

1. To review the contents of the **Software** registry key, in the **Windows PowerShell** console, enter the following command, and then press the Enter key:

   ```powershell
   Get-ChildItem -Path HKCU:\Software
   ```

1. Enter the following command, and then press the Enter key:

   ```powershell
   New-Item –Path HKCU:\Software –Name Scripts
   ```

### Task 2: Create a new registry value to store the name of the PSDrive

1. To change location to **HKCU:\Software\Scripts**, enter the following command, and then press the Enter key:

   ```powershell
   Set-Location HKCU:\Software\Scripts
   ```

1. To create a **PSDriveName** registry value, enter the following command, and then press the Enter key:

   ```powershell
   New-ItemProperty -Path HKCU:\Software\Scripts -Name "PSDriveName" –Value "ScriptShare"
   ```

1. To review the PSDriveName registry value, enter the following command, and then press the Enter key:

   ```powershell
   Get-ItemProperty . -Name PSDriveName
   ```

## Exercise 3: Creating a new Active Directory group

### Task 1: Create a PSDrive that maps to the Users container in AD DS

1. To load the **ActiveDirectory** module, in the **Windows PowerShell** console, enter the following command, and then press the Enter key:

   ```powershell
   Import-Module ActiveDirectory
   ```

1. To create a new **AdatumUsers** PSDrive, enter the following command, and then press the Enter key:

   ```powershell
   New-PSDrive -Name AdatumUsers -Root "CN=Users,DC=Adatum,DC=com" -PSProvider ActiveDirectory
   ```

1. To change location to the **AdatumUsers** drive, enter the following command, and then press the Enter key:

   ```powershell
   Set-Location AdatumUsers:
   ```

### Task 2: Create the London Developers group

1. To create the London Developers group, enter the following command, and then press the Enter key:

   ```powershell
   New-Item -ItemType group -Path . -Name "CN=London Developers"
   ```

1. To list items in the current drive, enter the following command, and then press the Enter key:

   ```powershell
   Get-ChildItem
   ```

1. Verify that the **London Developers** group is listed.
