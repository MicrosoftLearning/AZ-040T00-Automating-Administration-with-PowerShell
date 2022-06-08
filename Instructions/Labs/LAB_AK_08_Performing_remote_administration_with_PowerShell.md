---
lab:
    title: 'Lab: Performing remote administration with PowerShell'
    type: 'Answer Key'
    module: 'Module 8: Administering remote computers with Windows PowerShell'
---

# Lab answer key: Performing remote administration with PowerShell

## Exercise 1: Enabling remoting on the local computer

### Task 1: Enable remoting for incoming connections

1. Ensure that you're signed in to the **LON-CL1** virtual machine as **Adatum\\Administrator** with the password **Pa55w.rd**.

1. Select the **Start** menu, and then enter **powersh**.

1. In the results list, right-click **Windows PowerShell** or activate its context menu, and select **Run as administrator**.

1. To ensure you have the correct execution policy in place, in the Windows PowerShell command window, enter the following command, and then press the Enter key:

   ```powershell
   Set-ExecutionPolicy RemoteSigned
   ```

1. Select **Yes** or enter **Y** to confirm the change.

1. On the **LON-CL1** computer, run the following command:

   ```powershell
   Enable-PSremoting -SkipNetworkProfileCheck
   ```

   If prompted, answer Yes to all prompts by selecting **Y**. This will enable remoting.

1. To find a command that can list session configurations, enter the following command, and then press the Enter key:

   ```powershell
   help *sessionconfiguration*
   ```

   > **Note:** Notice the **Get-PSSessionConfiguration** command.

1. To list session configurations, enter the following command, and then press the Enter key:

   ```powershell
   Get-PSSessionConfiguration
   ```

1. Verify that two to four session configurations were created. Leave the Windows PowerShell window open.

## Exercise 2: Performing one-to-one remoting

### Task 1: Connect to the remote computer and install an operating system feature on it

1. Ensure that you're still signed in to the **LON-CL1** virtual machine as **Adatum\\Administrator** with the password **Pa55w.rd**.
1. On **LON-CL1**, to establish a one-to-one connection to **LON-DC1**, enter the following command in Windows PowerShell, and then press the Enter key:

   ```powershell
   Enter-PSSession –ComputerName LON-DC1
   ```

1. After you're connected, to install the Network Load Balancing (NLB) feature on **LON-DC1**, enter the following command, and then press the Enter key:

   ```powershell
   Install-WindowsFeature NLB
   ```

1. Wait for the command to complete.
1. To disconnect, enter the following command, and then press the Enter key:

   ```powershell
   Exit-PSSession
   ```

### Task 2: Test multi-hop remoting

1. To establish a one-to-one remoting connection to **LON-DC1**, enter the following command, and then press the Enter key:

   ```powershell
   Enter-PSSession –ComputerName LON-DC1
   ```

2. To establish a connection from **LON-DC1** to **LON-CL1**, enter the following command, and then press the Enter key:

   ```powershell
   Enter-PSSession –ComputerName LON-CL1
   ```

   > **Note:** You should receive an error that's indicative of the second hop. By default, you cannot establish a connection through an already-established connection.

3. To close the connection, enter the following command, and then press the Enter key:

   ```powershell
   Exit-PSSession
   ```

### Task 3: Observe remoting limitations

1. Ensure that you're signed in to the **LON-CL1** virtual machine as **Adatum\\Administrator** with the password **Pa55w.rd**.
1. To establish a one-to-one connection to **LON-CL1**, enter the following command, and then press the Enter key:

   ```powershell
   Enter-PSSession –ComputerName localhost
   ```

1. Enter the following command, and then press the Enter key:

   ```powershell
   Notepad
   ```

   > **Note:** Notice that the shell seems to stop responding while it waits for Notepad to open, because Notepad is a graphical application, and the shell has no way to display the graphical user interface (GUI).

1. Select **Ctrl+C** to cancel the process and return to a shell prompt.
1. To disconnect, enter the following command, and then press the Enter key:

   ```powershell
   Exit-PSSession
   ```

## Exercise 3: Performing one-to-many remoting

### Task 1: Retrieve a list of physical network adapters from two computers

1. Ensure that you're still signed in to the **LON-CL1** virtual machine as **Adatum\\Administrator** with the password **Pa55w.rd**.
1. On **LON-CL1**, to find a command that can list network adapters, enter the following command in the Windows PowerShell window, and then press the Enter key:

   ```powershell
   help *adapter*
   ```

   > **Note:** Note the **Get-NetAdapter** command.

1. To review the Help for the command, enter the following command, and then press the Enter key:

   ```powershell
   help Get-NetAdapter 
   ```

    > **Note:** Note the *–Physical* parameter.

1. To run the command on **LON-DC1** and **LON-CL1** by means of remoting, enter the following command, and then press the Enter key:

   ```powershell
   Invoke-Command –ComputerName LON-CL1,LON-DC1 –ScriptBlock { Get-NetAdapter –Physical }
   ```

### Task 2: Compare the output of a local command to that of a remote command

1. To review the members of a **Process** object, enter the following command, and then press the Enter key:

   ```powershell
   Get-Process | Get-Member
   ```

1. To review the members from a remote Process object, enter the following command, and then press the Enter key:

   ```powershell
   Invoke-Command –ComputerName LON-DC1 –ScriptBlock { Get-Process } | Get-Member
   ```

   > **Note:** The second set of results only includes two **MemberType** of **Methods; GetType**, and **ToString**. This is because the remote value **TypeName** is deserialized in comparison to the local output.

## Exercise 4: Using implicit remoting

### Task 1: Create a persistent remoting connection to a server

1. On **LON-CL1**, ensure that you're signed in as **Adatum\\Administrator** with the password **Pa55w.rd**.
1. If the Windows PowerShell window is closed, select the **Start** menu, and then enter **powersh**.
1. In the results list, right-click **Windows PowerShell** or activate its context menu, and then select **Run as administrator**.
1. In the Windows PowerShell command window, create a persistent connection to **LON-DC1** and store it in a variable. Enter the following command, and then press the Enter key:

   ```powershell
   $dc = New-PSSession –ComputerName LON-DC1
   ```

1. To review the PSSession list in the variable, enter the following command, and then press the Enter key:

   ```powershell
   $dc
   ```

   > **Note:** Verify that the connection is available.

### Task 2: Import and use a module from a server

1. To display a list of modules on **LON-DC1**, enter the following command, and then press the Enter key:

   ```powershell
   Get-Module –ListAvailable –PSSession $dc
   ```

1. To find a module on **LON-DC1** that can work with Server Message Block (SMB) shares, enter the following command, and then press the Enter key:

   ```powershell
   Get-Module –ListAvailable –PSSession $dc | Where { $_.Name –Like '*share*' }
   ```

1. To import the module from **LON-DC1** to your local computer, and to add the prefix **DC** to the important commands’ nouns, enter the following command, and then press the Enter key:

   ```powershell
   Import-Module –PSSession $dc –Name SMBShare –Prefix DC
   ```

1. To display a list of shares on **LON-DC1**, enter the following command, and then press the Enter key:

   ```powershell
   Get-DCSMBShare
   ```

   > **Note:** Because this command implicitly runs on **LON-DC1**, the command will display shares on that computer.

1. To display a list of shares on the local computer, enter the following command, and then press the Enter key:

   ```powershell
   Get-SMBShare
   ```

   > **Note:** Because you added the DC prefix to the imported commands, the local commands are still available by their original name.

### Task 3: Close all open remoting connections

1. In the Windows PowerShell command window, enter the following command, and then press the Enter key:

   ```powershell
   Get-PSSession | Remove-PSSession
   ```

2. Note that the command to verify that the remoting session has been closed isn't explicitly called out in the sample answer script provided at **E:\\Mod08\\Labfiles\\ImplicitRemoting.ps1.txt**. To verify the remoting connection has been closed, enter the following command, and then press the Enter key:

   ```powershell
   Get-PSSession
   ```

   > **Note:** Verify that no sessions are returned.

## Exercise 5: Managing multiple computers

### Task 1: Create PSSessions to two computers

1. Ensure that you're still signed in to **LON-CL1** as **Adatum\\Administrator** with the password **Pa55w.rd**.

2. Open Windows PowerShell if it's not already open.

3. To create PSSessions to **LON-CL1** and **LON-DC1**, and to save those in a variable, enter the following command, and then press the Enter key:

   ```powershell
   $computers = New-PSSession –ComputerName LON-CL1,LON-DC1
   ```

4. To verify the connections, enter the following command, and then press the Enter key:

   ```powershell
   $computers
   ```

   > **Note:** Verify that two connections display as available.

### Task 2: Create a report that displays Windows Firewall rules from two computers

1. To find a module capable of working with network security, enter the following command, and then press the Enter key:

   ```powershell
   Get-Module *security* –ListAvailable
   ```

1. Note the **Net-Security** module in the list.
1. To load the module into memory on **LON-CL1** and **LON-DC1**, enter the following command, and then press the Enter key:

   ```powershell
   Invoke-Command –Session $computers –ScriptBlock { Import-Module NetSecurity }
   ```

1. To find a command that can display Windows Firewall rules, enter the following command, and then press the Enter key:

   ```powershell
   Get-Command –Module NetSecurity
   ```

   > **Note:** Observe the **Get-NetFirewallRule** command.

1. If you want to review the Help for the command, enter the following command, and then press the Enter key:

   ```powershell
   Help Get-NetFirewallRule -ShowWindow
   ```

   > **Note:** If Help isn't displaying correctly, run the commands from steps 1 to 3 in the Windows PowerShell command window as administrator rather than in Windows PowerShell ISE.

1. Close the **Get-NetFirewallRule Help** window.

1. To display a list of enabled firewall rules on **LON-DC1** and **LON-CL1**, enter the following command, and then press the Enter key:

   ```powershell
   Invoke-Command –Session $computers –ScriptBlock { Get-NetFirewallRule –Enabled True } | Select Name,PSComputerName
   ```

1. To unload the module on **LON-DC1** and **LON-CL1**, enter the following command, and then press the Enter key:

   ```powershell
   Invoke-Command –Session $computers –ScriptBlock { Remove-Module NetSecurity }
   ```

### Task 3: Create and display an HTML report that displays local disk information from two computers

1. To display a list of local hard drives filtered to include only those with a drive type of **3**, enter the following command, and then press the Enter key:

   ```powershell
   Get-WmiObject –Class Win32_LogicalDisk –Filter "DriveType=3"
   ```

1. To run the same command on **LON-DC1** and **LON-CL1** by means of remoting, enter the following command, and then press the Enter key:

   ```powershell
   Invoke-Command –Session $computers –ScriptBlock { Get-WmiObject –Class Win32_LogicalDisk –Filter "DriveType=3" }
   ```

   > **Note:** Your report must include each computer’s name, each drive’s letter, and each drive’s free space and total size in bytes.

1. To produce an HTML report containing the results of the previous command, enter the following command, and then press the Enter key:

   ```powershell
   Invoke-Command –Session $computers –ScriptBlock { Get-WmiObject –Class Win32_LogicalDisk –Filter "DriveType=3" } | ConvertTo-Html –Property PSComputerName,DeviceID,FreeSpace,Size
   ```

### Task 4: Close all open PSSessions

- To close all open PSSessions, enter the following command, and then press the Enter key:

   ```powershell
   Get-PSSession | Remove-PSSession
   ```
