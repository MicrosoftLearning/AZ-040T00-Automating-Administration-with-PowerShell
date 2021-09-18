---
lab:
    title: 'Lab: Using PSProviders and PSDrives with PowerShell'
    module: 'Module 4: Using PSProviders and PSDrives'
---

# Lab: Using PSProviders and PSDrives with PowerShell

## Scenario

You're a system administrator for the London branch office of Adatum Corporation. You must reconfigure several settings in your environment. You've recently learned about PSProviders and PSDrives, and that you can use them to access data stores. You've decided to use PSDrives to reconfigure these settings.

## Objectives

After completing this lab, you'll be able to:

- Use a PSDrive to create files and folders.
- Create registry keys and values.
- Use a PSDrive to create and view Active Directory objects.

## Estimated time: 30 minutes

## Lab Setup

Virtual machines:

- **LON-DC1**
- **LON-SVR1**
- **LON-CL1**

Username: **Adatum\\Administrator**

Password: **Pa55w.rd**

For this lab, you'll use the available virtual machine environment. Before you begin the lab, complete the following steps:

1. Open **LON-DC1**, and then sign in as **Adatum\\Administrator** with the password **Pa55w.rd**.
1. Repeat step 1 for **LON-SVR1**, and **LON-CL1**.

## Exercise 1: Creating files and folders on a remote computer

### Exercise scenario 1

You need to make sure that you can create folders and files on a remote computer so that you're able to copy automation scripts to the computer in the future. You've decided not to use the **MkDir** command or any of its aliases so you can be sure that you're using the cmdlets associated with PSProviders and PSDrives.

The main tasks for this exercise are as follows:

1. Create a new folder on a remote computer.
1. Create a new PSDrive mapping to the remote file folder.
1. Create a file on the mapped drive.

### Task 1: Create a new folder on a remote computer

1. On **LON-CL1**, open Windows PowerShell as an administrator.
1. Review the complete help for the **New-Item** cmdlet. Notice the *–Name* and *–ItemType* parameters, and then review the example commands.
1. Use **New-Item** to create a new folder (directory) named **ScriptShare** on **\\\LON-SVR1\C$**.

### Task 2: Create a new PSDrive mapping to the remote file folder

1. In the Windows PowerShell console, review the complete help for the **New-PSDrive** command.
1. Create a new PSDrive named **ScriptShare**, which is mapped to **\\\LON-SVR1\C$\ScriptShare**.

### Task 3: Create a file on the mapped drive

1. In the Windows PowerShell console, review the complete help for the **Set-Location** cmdlet.
1. Set the current working folder location to the mapped drive **ScriptShare**.
1. In the **ScriptShare** drive, use the **New-Item** cmdlet to create a text file named **script.txt**.
1. List the items in the **ScriptShare** drive and confirm that it contains the **script.txt** file.

## Exercise 2: Creating a registry key for your future scripts

### Scenario 2

In this exercise, you will create a new registry key to store configuration data for scripts that you'll develop in the future. You'll also create a registry value in that key where you'll store the name of the PSDrive for the scripts to use. You want to verify that you can retrieve the value from the registry in scripts that you'll create later.

The main tasks for this exercise are as follows:

1. Create the registry key to store script configurations.
1. Create a new registry value to store the name of the PSDrive.

### Task 1: Create the registry key to store script configurations

1. In the **Windows PowerShell** console, enter a command to verify that the registry key **HKEY_CURRENT_USER\Software** does not have a subkey named **Scripts**.
1. In the console, run a command to create a registry key named **Scripts** in **HKEY_CURRENT_USER\Software**.

### Task 2: Create a new registry setting to store the name of the PSDrive

1. In the **Windows PowerShell** console, run a command to set the current working location to the path of the registry key that you created.
1. Create a registry value to store the PSDrive name with the following configuration:

   - Name: **PSDriveName**
   - Value: **ScriptShare**

1. Verify that you can retrieve the **PSDriveName** setting from the **HKey_Current_User\Software\Scripts** key.

## Exercise 3: Creating a new Active Directory group

You want the ability to manage all AD DS object types through a PSDrive that's mapped to the User organizational unit in Active Directory. This PSDrive will use the ActiveDirectory provider. Once the new PSDrive is mapped, you want to create a new London Developers group that you can use to assign permissions to the developers in the London office.

The main tasks for this exercise are as follows:

1. Create a PSDrive that maps to the Users container in AD DS.
1. Create the London Developers group.

### Task 1: Create a PSDrive that maps to the Users container in AD DS

1. In the **Windows PowerShell** console, load the **ActiveDirectory** module.
1. Use the **New-PSDrive** cmdlet to create a new PSDrive with the following settings:

   - Name: **AdatumUsers**
   - Root: **CN=Users,DC=Adatum,DC=com**
   - PSProvider: **ActiveDirectory**

1. Set the current working location to the new PSDrive.

### Task 2: Create the London Developers group

1. In the **Windows PowerShell** console, use the **New-Item** cmdlet to create a group named **London Developers** in the **AdatumUsers** PSDrive.
1. Use the **Get-ChildItem** cmdlet to verify that the new group was created.
