---
lab:
    title: 'Lab: Using PowerShell pipeline'
    type: 'Answer Key'
    module: 'Module 3: Working with the Windows PowerShell pipeline'
---

# Lab: Using PowerShell pipeline

## Exercise 1: Selecting, sorting, and displaying data

### Task 1: Display the current day of the year

1. On **LON-CL1**, select **Start**, and then enter **PowerShell**.
1. In the search results, right-click **Windows PowerShell** or activate its context menu, and then select **Run as administrator**.
1. In the **Administrator: Windows PowerShell** window, enter the following command, and then select Enter:

   ```powershell
   help *date* 
   ```

   > **Note:** Notice the **Get-Date** command.

1. In the console, enter the following command, and then select Enter:  

   ```powershell
   Get-Date | Get-Member
   ```

   > **Note:** Notice the **DayOfYear** property.

1. In the console, enter the following command, and then select Enter:

   ```powershell
   Get-Date | Select-Object –Property DayOfYear
   ```

1. In the console, enter the following command, and then select Enter:

   ```powershell
   Get-Date | Select-Object -Property DayOfYear | fl
   ```

### Task 2: Display information about installed hotfixes

1. In the console, enter the following command, and then select Enter:

   ```powershell
   Get-Command *hotfix* 
   ```

   > **Note:** Notice the **Get-Hotfix** command.

1. In the console, enter the following command, and then select Enter:

   ```powershell
   Get-Hotfix | Get-Member 
   ```

   > **Note:** The properties of the **Hotfix** object display. If needed, run **Get-Hotfix** to review some of the values that typically display in those properties.

1. In the console, enter the following command, and then select Enter:  

   ```powershell
    Get-Hotfix | Select-Object –Property HotFixID,InstalledOn,InstalledBy
   ```

1. In the console, enter the following command, and then select Enter:

   ```powershell
   Get-Hotfix | Select-Object –Property HotFixID,@{n='HotFixAge';e={(New-TimeSpan -Start $PSItem.InstalledOn).Days}},InstalledBy
   ```

### Task 3: Display a list of available scopes from the DHCP server

1. In the console, enter the following command, and then select Enter:

   ```powershell
   help *scope* 
   ```

   > **Note:** Notice the **Get-DHCPServerv4Scope** command.

1. In the console, enter the following command, and then select Enter:

   ```powershell
   Help Get-DHCPServerv4Scope –ShowWindow 
   ```

   > **Note:** Notice the available parameters.

1. In the console, enter the following command, and then select Enter:

   ```powershell
   Get-DHCPServerv4Scope –ComputerName LON-DC1
   ```

1. In the console, enter the following command, and then select Enter:

   ```powershell
   Get-DHCPServerv4Scope –ComputerName LON-DC1 | Select-Object –Property ScopeId,SubnetMask,Name | fl
   ```

### Task 4: Display a sorted list of enabled Windows Firewall rules

1. In the console, enter the following command, and then select Enter:

      ```powershell
      help *rule* 
      ```

   > **Note:** Notice the **Get-NetFirewallRule** command.

1. In the console, enter the following command, and then select Enter:

      ```powershell
      Get-NetFirewallRule 
      ```

1. In the console, enter the following command, and then select Enter:

      ```powershell
      Help Get-NetFirewallRule –ShowWindow
      ```
  
1. In the console, enter the following command, and then select Enter:

      ```powershell
      Get-NetFirewallRule –Enabled True

      ```

1. In the console, enter the following command, and then select Enter:
  
      ```powershell
      Get-NetFirewallRule –Enabled True | Format-Table -wrap
      ```

1. In the console, enter the following command, and then select Enter:

      ```powershell
      Get-NetFirewallRule –Enabled True | Select-Object –Property DisplayName,Profile,Direction,Action | Sort-Object –Property Profile, DisplayName | ft -GroupBy Profile
      ```

### Task 5: Display a sorted list of network neighbors

1. In the console, enter the following command, and then select Enter:

      ```powershell
      help *neighbor*  
      ```

   > **Note:** Notice the **Get-NetNeighbor** command.

1. In the console, enter the following command, and then select Enter:

      ```powershell
      help Get-NetNeighbor –ShowWindow
      ```

1. In the console, enter the following command, and then select Enter:

      ```powershell
      Get-NetNeighbor
      ```

1. In the console, enter the following command, and then select Enter:

      ```powershell
      Get-NetNeighbor | Sort-Object –Property State
      ```

1. In the console, enter the following command, and then select Enter:

      ```powershell
      Get-NetNeighbor | Sort-Object –Property State | Select-Object –Property IPAddress,State | Format-Wide -GroupBy State -AutoSize
      ```

### Task 6: Display information from the DNS name resolution cache

1. In the console, enter the following command, and then select Enter:

      ```powershell
      Test-NetConnection LON-DC1
      ```

1. In the console, enter the following command, and then select Enter:

      ```powershell
      help *cache* 
      ```

      > **Note:** Notice the **Get-DnsClientCache** command.

1. In the console, enter the following command, and then select Enter:

      ```powershell
      Get-DnsClientCache
      ```

1. In the console, enter the following command, and then select Enter:

      ```powershell
      Get-DnsClientCache | Select Name,Type,TimeToLive | Sort Name | Format-List
      ```

      > **Note:** Notice that the **Type** data doesn't return what you might expect; for example, A and CNAME. Instead, it returns raw numerical data. Each number maps directly to a record type, and you can filter for those types when you know the map: 1= A, 5 = CNAME, and so on. Later in this module, you'll learn how to add more filters to determine the numbers and their corresponding record types. You'll notice a similar situation for other returned data, such as **Status** data.

1. Close all open windows.

### Exercise 1 results

After completing this exercise, you should have produced several custom reports that contain management information from your environment.

## Exercise 2: Filtering objects

### Task 1: Display a list of all the users in the Users container of Active Directory

1. On **LON-CL1**, select **Start**, and then enter **PowerShell**.
1. In the search results, right-click **Windows PowerShell** or activate its context menu, and then select **Run as administrator**.
1. In the **Administrator: Windows PowerShell** window, enter the following command, and then select Enter:

   ```powershell
   help *user*
   ```

   > **Note:** Notice the **Get-ADUser** command.

1. In the console, enter the following command, and then select Enter:

   ```powershell
   Get-Help Get-ADUser –ShowWindow
   ```

   > **Note:** Notice that the *-Filter* parameter is mandatory. Review the examples for the command.
  
1. In the console, enter the following command, and then select Enter:

   ```powershell
   Get-ADUser –Filter * | ft
   ```

1. In the console, enter the following command, and then select Enter:

   ```powershell
   Get-ADUser –Filter * -SearchBase "cn=Users,dc=Adatum,dc=com" | ft
   ```

### Task 2: Create a report of the Security event log entries that have the event ID 4624

1. In the **Administrator: Windows PowerShell** window, enter the following command, and then select Enter:

   ```powershell
   Get-EventLog -LogName Security | 
   Where EventID -eq 4624 | Measure-Object | fw
   ```

1. In the console, enter the following command and select Enter:

   ```powershell
   Get-EventLog -LogName Security | 
   Where EventID -eq 4624 | 
   Select TimeWritten,EventID,Message
   ```

1. In the console, enter the following command, and then select Enter:

   ```powershell
   Get-EventLog -LogName Security | 
   Where EventID -eq 4624 | 
   Select TimeWritten,EventID,Message -Last 10 | fl
   ```

### Task 3: Display a list of the encryption certificates installed on the computer

1. In the **Administrator: Windows PowerShell** window, enter the following command, and then select Enter:

   ```powershell
   Get-ChildItem -Path CERT: -Recurse
   ```

1. In the console, enter the following command, and then select Enter:

   ```powershell
   Get-ChildItem -Path CERT: -Recurse | 
   Get-Member
   ```

1. In the console window, enter the following command, and then select Enter.

   ```powershell
   Get-ChildItem -Path CERT: -Recurse | 
   Where HasPrivateKey -eq $False | Select-Object -Property FriendlyName,Issuer | fl
   ```

   or:

   ```powershell
   Get-ChildItem -Path CERT: -Recurse | 
   Where { $PSItem.HasPrivateKey -eq $False } | Select-Object -Property FriendlyName,Issuer | fl
   ```

1. In the console window, enter the following command, and then select Enter.

   ```powershell
   Get-ChildItem -Path CERT: -Recurse | 
   Where { $PSItem.HasPrivateKey -eq $False -and $PSItem.NotAfter -gt (Get-Date) -and $PSItem.NotBefore -lt (Get-Date) } | Select-Object -Property NotBefore,NotAfter, FriendlyName,Issuer | ft -wrap
   ```

### Task 4: Create a report of the disk volumes that are running low on space

1. In the **Administrator: Windows PowerShell** window, enter the following command, and then select Enter:

   ```powershell
   Get-Volume
   ```

   > **Note:** If you didn't know the command name, you could have run **Help \*volume\*** to discover it.

1. In the console, enter the following command, and then select Enter:

   ```powershell
   Get-Volume | Get-Member
   ```

   > **Note:** Notice the **SizeRemaining** property.

1. In the console, enter the following command, and then select Enter:

   ```powershell
   Get-Volume | Where-Object { $PSItem.SizeRemaining -gt 0 } | fl
   ```

1. In the console, enter the following command, and then select Enter:

   ```powershell
   Get-Volume | Where-Object { $PSItem.SizeRemaining -gt 0 -and $PSItem.SizeRemaining / $PSItem.Size -lt .99 }| Select-Object DriveLetter, @{n='Size';e={'{0:N2}' -f ($PSItem.Size/1MB)}}
   ```

1. In the console, enter the following command, and then select Enter:

   ```powershell
   Get-Volume | Where-Object { $PSItem.SizeRemaining -gt 0 -and $PSItem.SizeRemaining / $PSItem.Size -lt .1 }
   ```

   > **Note:** This command might not produce any output on your lab computer if the computer has more than 10 percent free space on each of its volumes.

### Task 5: Create a report that displays specified Control Panel items

1. In the **Administrator: Windows PowerShell** window, enter the following command, and then select Enter:

   ```powershell
   help *control* 
   ```

   > **Note:** Notice the **Get-ControlPanelItem** command.

1. In the console, enter the following command, and then select Enter:

   ```powershell
   Get-ControlPanelItem 
   ```

1. In the console, enter the following command, and then select Enter:

   ```powershell
   Get-ControlPanelItem –Category 'System and Security' | Sort Name
   ```

    > **Note:** Notice that you don't have to use **Where-Object**.

1. In the console, enter the following command, and then select Enter:

   ```powershell
   Get-ControlPanelItem -Category 'System and Security' | Where-Object -FilterScript {-not ($PSItem.Category -notlike '*System and Security*')} | Sort Name
   ```

### Exercise 2 results

After completing this exercise, you should have used filtering to produce lists of management information that include only specified data and elements.

## Exercise 3: Enumerating objects

### Task 1: Display a list of files on drive E of your computer

1. On **LON-CL1**, select **Start** and then enter **PowerShell**.
1. In the search results, right-click **Windows PowerShell** or activate its context menu, and then select **Run as administrator**.
1. In the **Administrator: Windows PowerShell** window, enter the following command, and then select Enter:

   ```powershell
   Get-ChildItem -Path E: -Recurse
   ```

1. In the console, enter the following command, and then select Enter:

   ```powershell
   Get-ChildItem -Path E: -Recurse | Get-Member 
   ```

   > **Note:** Notice the **GetFiles** method in the list under **TypeName: System.IO.DirectoryInfo**.

1. In the console, enter the following command, and then select Enter:

   ```powershell
   Get-ChildItem -Path E: -Recurse | ForEach GetFiles
   ```

### Task 2: Use enumeration to produce 100 random numbers

1. In the console, enter the following command, and then select Enter:

   ```powershell
   help *random* 
   ```

   > **Note:** Notice the **Get-Random** command.

1. In the console, enter the following command, and then select Enter:

   ```powershell
   help Get-Random –ShowWindow 
   ```

   > **Note:** Notice the *-SetSeed* parameter.

1. In the console, enter the following command, and then select Enter:

   ```powershell
   1..100 
   ```

1. In the console, enter the following command, and then select Enter:

   ```powershell
   1..100 | 
   ForEach { Get-Random –SetSeed $PSItem }
   ```

### Task 3: Run a method of a Windows Management Instrumentation (WMI) object

1. Close all applications other than the **Windows PowerShell console**.
1. In the console, enter the following command, and then select Enter:

   ```powershell
   Get-WmiObject –Class Win32_OperatingSystem -EnableAllPrivileges
   ```

1. In the console, enter the following command, and then select Enter:

   ```powershell
   Get-WmiObject –Class Win32_OperatingSystem -EnableAllPrivileges | 
   Get-Member
   ```

   > **Note:** Notice the **Reboot** method.

   > **Note:** The following command will reboot the machine you run it on.

1. In the console, enter the following command, and then select Enter:

   ```powershell
   Get-WmiObject –Class Win32_OperatingSystem -EnableAllPrivileges | 
   ForEach Reboot
   ```

### Exercise 3 results

After completing this exercise, you should have created commands that manipulate multiple objects in the pipeline.

## Exercise 4: Converting objects

### Task 1: Update Active Directory user information

> **Note:** In this lab, long commands typically display on several lines. This helps to prevent unintended line breaks in the middle of commands. However, when you enter these commands, you should enter them as a single line. That line might wrap on your screen into multiple lines, but the command will still work. Select Enter only after entering the entire command.

1. Sign in to the **LON-CL1** as **Adatum\\Administrator** with the password **Pa55w.rd.**
1. On **LON-CL1**, select **Start**, and then enter **PowerShell**.
1. In the search results, right-click **Windows PowerShell** or activate its context menu, and then select **Run as administrator**.
1. In the **Administrator: Windows PowerShell** window, enter the following command, and then select Enter:

   ```powershell
   Get-ADUser -Filter * -Properties Department,City | Where {$PSItem.Department -eq ‘IT’ -and $PSItem.City -eq ‘London’} | Select-Object -Property Name,Department,City| Sort Name
   ```

1. In the **Administrator: Windows PowerShell** window, enter the following command, and then select Enter:

   ```powershell
   Get-ADUser -Filter * -Properties Department,City | Where {$PSItem.Department -eq ‘IT’ -and $PSItem.City -eq ‘London’} | Set-ADUser -Office ‘LON-A/1000’
   ```

1. In the **Administrator: Windows PowerShell** window, enter the following command, and then select Enter:

   ```powershell
   Get-ADUser -Filter * -Properties Department,City,Office | Where {$PSItem.Department -eq ‘IT’ -and $PSItem.City -eq ‘London’} | Select-Object -Property Name,Department,City,Office | Sort Name
   ```

### Task 2: Produce an HTML report listing the Active Directory users in the IT department

1. In the console, enter the following command, and then select Enter:

   ```powershell
   help ConvertTo-Html –ShowWindow
   ```

1. In the console, enter the following command, and then select Enter:

   ```powershell
   Get-ADUser -Filter * -Properties Department,City,Office | 
   Where {$PSItem.Department -eq 'IT' -and $PSItem.City -eq 'London'} | 
   Sort Name | 
   Select-Object -Property Name,Department,City,Office |
   ConvertTo-Html –Property Name,Department,City -PreContent Users | 
   Out-File E:\UserReport.html
   ```

1. To review the HTML file, enter the following command, and then select Enter:

   ```powershell
   Invoke-Expression E:\UserReport.html
   ```

1. In the console, enter the following command, and then select Enter:

   ```powershell
   Get-ADUser -Filter * -Properties Department,City,Office | 
   Where {$PSItem.Department -eq 'IT' -and $PSItem.City -eq 'London'} | 
   Sort Name | 
   Select-Object -Property Name,Department,City,Office |
   Export-Clixml E:\UserReport.xml
   ```

1. In Internet Explorer, in the address bar, enter **E:\\UserReport.xml**, and then select Enter.
1. In the console, enter the following command, and then select Enter:

   ```powershell
   Get-ADUser -Filter * -Properties Department,City,Office | 
   Where {$PSItem.Department -eq 'IT' -and $PSItem.City -eq 'London'} | 
   Sort Name | 
   Select-Object -Property Name,Department,City,Office |
   Export-Csv E:\UserReport.csv
   ```

1. In File Explorer, refer to **E:\\**, right-click **UserReport.csv** or activate its context menu, select **Open with**, and then select **Notepad**.
1. In File Explorer, refer to **E:\\**, select **UserReport.csv**, and then select Enter.

### Exercise 4 results

After completing this exercise, you should have converted Active Directory user objects to different data formats.
