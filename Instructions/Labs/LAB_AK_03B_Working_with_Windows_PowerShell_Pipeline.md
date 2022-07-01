---
lab:
    title: 'Lab: Using PowerShell pipeline'
    type: 'Answer Key'
    module: 'Module 3: Working with the Windows PowerShell pipeline'
---

# Lab answer key: Using PowerShell pipeline

## Exercise 1: Enumerating objects

### Task 1: Display a list of files on drive E of your computer

1. On **LON-CL1**, select **Start** and then enter **powersh**.
1. In the search results, right-click **Windows PowerShell** or activate its context menu, and then select **Run as administrator**.
1. In the **Administrator: Windows PowerShell** window, enter the following command, and then press the Enter key:

   ```powershell
   Get-ChildItem -Path E: -Recurse
   ```

1. In the console, enter the following command, and then press the Enter key:

   ```powershell
   Get-ChildItem -Path E: -Recurse | Get-Member 
   ```

   > **Note:** Notice the **GetFiles** method in the list under **TypeName: System.IO.DirectoryInfo**.

1. In the console, enter the following command, and then press the Enter key:

   ```powershell
   Get-ChildItem -Path E: -Recurse | ForEach GetFiles
   ```

### Task 2: Use enumeration to produce 100 random numbers

1. In the console, enter the following command, and then press the Enter key:

   ```powershell
   help *random* 
   ```

   > **Note:** Notice the **Get-Random** command.

1. In the console, enter the following command, and then press the Enter key:

   ```powershell
   help Get-Random –ShowWindow 
   ```

   > **Note:** Notice the *-SetSeed* parameter.

1. Close the **Get-Random Help** window.  
1. In the console, enter the following command, and then press the Enter key:

   ```powershell
   1..100 
   ```

1. In the console, enter the following command, and then press the Enter key:

   ```powershell
   1..100 | 
   ForEach { Get-Random –SetSeed $PSItem }
   ```

### Task 3: Run a method of a Windows Management Instrumentation (WMI) object

1. Close all applications other than the **Windows PowerShell** console.
1. In the console, enter the following command, and then press the Enter key:

   ```powershell
   Get-WmiObject –Class Win32_OperatingSystem -EnableAllPrivileges
   ```

1. In the console, enter the following command, and then press the Enter key:

   ```powershell
   Get-WmiObject –Class Win32_OperatingSystem -EnableAllPrivileges | 
   Get-Member
   ```

   > **Note:** Notice the **Reboot** method.

   > **Note:** The following command will reboot the machine you run it on.

1. In the console, enter the following command, and then press the Enter key:

   ```powershell
   Get-WmiObject –Class Win32_OperatingSystem -EnableAllPrivileges | 
   ForEach Reboot
   ```

### Exercise 1 results

After completing this exercise, you should have created commands that manipulate multiple objects in the pipeline.

## Exercise 2: Converting objects

### Task 1: Update Active Directory user information

> **Note:** In this lab, long commands typically display on several lines. This helps to prevent unintended line breaks in the middle of commands. However, when you enter these commands, you should enter them as a single line. That line might wrap on your screen into multiple lines, but the command will still work. press the Enter key only after entering the entire command.

1. Sign in to the **LON-CL1** as **Adatum\\Administrator** with the password **Pa55w.rd.**
1. On **LON-CL1**, select **Start**, and then enter **powersh**.
1. In the search results, right-click **Windows PowerShell** or activate its context menu, and then select **Run as administrator**.
1. In the **Administrator: Windows PowerShell** window, enter the following command, and then press the Enter key:

   ```powershell
   Get-ADUser -Filter * -Properties Department,City | Where {$PSItem.Department -eq ‘IT’ -and $PSItem.City -eq ‘London’} | Select-Object -Property Name,Department,City| Sort Name
   ```

1. In the **Administrator: Windows PowerShell** window, enter the following command, and then press the Enter key:

   ```powershell
   Get-ADUser -Filter * -Properties Department,City | Where {$PSItem.Department -eq ‘IT’ -and $PSItem.City -eq ‘London’} | Set-ADUser -Office ‘LON-A/1000’
   ```

1. In the **Administrator: Windows PowerShell** window, enter the following command, and then press the Enter key:

   ```powershell
   Get-ADUser -Filter * -Properties Department,City,Office | Where {$PSItem.Department -eq ‘IT’ -and $PSItem.City -eq ‘London’} | Select-Object -Property Name,Department,City,Office | Sort Name
   ```

### Task 2: Generate files listing the Active Directory users in the IT department

1. In the console, enter the following command, and then press the Enter key:

   ```powershell
   help ConvertTo-Html –ShowWindow
   ```

1. Close the **ConvertTo-Html Help** window.  
1. In the console, enter the following command, and then press the Enter key:

   ```powershell
   Get-ADUser -Filter * -Properties Department,City,Office | 
   Where {$PSItem.Department -eq 'IT' -and $PSItem.City -eq 'London'} | 
   Sort Name | 
   Select-Object -Property Name,Department,City,Office |
   ConvertTo-Html –Property Name,Department,City -PreContent Users | 
   Out-File E:\UserReport.html
   ```

1. To review the HTML file, enter the following command, and then press the Enter key:

   ```powershell
   Invoke-Expression E:\UserReport.html
   ```

1. In the console, enter the following command, and then press the Enter key (this will automatically open a web browser window):

   ```powershell
   Get-ADUser -Filter * -Properties Department,City,Office | 
   Where {$PSItem.Department -eq 'IT' -and $PSItem.City -eq 'London'} | 
   Sort Name | 
   Select-Object -Property Name,Department,City,Office |
   Export-Clixml E:\UserReport.xml
   ```

1. Review the report displayed on the web browser page and then close the web browser window. 
1. In the console, enter the following command, and then press the Enter key:

   ```powershell
   Get-ADUser -Filter * -Properties Department,City,Office | 
   Where {$PSItem.Department -eq 'IT' -and $PSItem.City -eq 'London'} | 
   Sort Name | 
   Select-Object -Property Name,Department,City,Office |
   Export-Csv E:\UserReport.csv
   ```

1. Open File Explorer, in the File Explorer window, navigate to **E:\\**, right-click **UserReport.csv** or activate its context menu, select **Open with**, and then select **Notepad**.
1. In the Notepad window, review the content of the file.

### Exercise 2 results

After completing this exercise, you should have queried Active Directory users, made changes to information about them, as well as converted Active Directory user objects to different data formats.

