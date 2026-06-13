---
lab:
  title: 'Lab: Using variables, arrays, and hash tables in PowerShell'
  type: Answer Key
  module: 'Module 6: Working with variables, arrays, and hash tables'
  description: Work with PowerShell variables, arrays, and hash tables to organize script data. You compare collection behaviors and choose the right structure for each task.
  duration: 45 minutes
  level: 200
  islab: true
  primarytopics:
    - Variables
    - Arrays
    - Hash Tables
    - PowerShell
---

# Using variables, arrays, and hash tables in PowerShell

This lab should take approximately **45** minutes to complete.

## Scenario

You're preparing to create scripts to automate server administration in your organization. Before you begin, you want to practice working with variables, arrays, and hash tables.

## Objectives

After completing this lab, you'll be able to:

- Work with variable types.
- Use arrays.
- Use hash tables.

## Lab setup

Virtual machines: **AZ-040T00A-LON-DC1**, **AZ-040T00A-LON-SVR1**, and **AZ-040T00A-LON-CL1**

Username: **Adatum\\Administrator**

Password: **Pa55w.rd**

For this lab, you'll use the available virtual machine environment. Before you begin the lab, complete the following steps:

1. Open **LON-DC1** and sign in as **Adatum\\Administrator** with the password **Pa55w.rd**.
1. Repeat step 1 for **LON-SVR1** and **LON-CL1**.

## Exercise 1: Working with variable types

### Exercise scenario 1

You first plan to practice working with different types of variables.

The main tasks for this exercise are:

1. Use string variables.
1. Use DateTime variables.

### Task 1: Use string variables

1. On **LON-CL1**, select **Start**, and then enter **powersh**.
1. In the results list, right-click **Windows PowerShell** or activate its context menu, and then select **Run as administrator**.
1. To set the `$logPath` variable, at the Windows PowerShell prompt, enter the following command, and then press the Enter key:

   ```powershell
   $logPath = "C:\Logs\"
   ```

1. To display the variable type for `$logPath`, enter the following command, and then press the Enter key:

   ```powershell
   $logPath.GetType()
   ```

1. To review the properties and methods for the `$logPath` variable, enter the following command, and then press the Enter key:

    ```powershell
    $logPath | Get-Member
    ```

1. To set the `$logFile` variable, enter the following command, and then press the Enter key:

    ```powershell
    $logFile = "log.txt"
    ```

1. To add the `$logFile` variable to the `$logPath` variable, enter the following command, and then press the Enter key:

    ```powershell
    $logPath += $logFile
    ```

1. To review the contents of the `$logPath` variable, enter the following command, and then press the Enter key:

    ```powershell
    $logPath
    ```

1. To replace **C:** with **D:** in the `$logPath` value, enter the following command, and then press the Enter key:

    ```powershell
    $logPath.Replace("C:","D:")
    ```

1. To replace **C:** with **D:** in `$logPath`, enter the following command, and then press the Enter key:

    ```powershell
    $logPath = $logPath.Replace("C:","D:")
    ```

1. To review the contents of the `$logPath` variable, enter the following command, and then press the Enter key:

     ```powershell
     $logPath
     ```

1. Leave the Windows PowerShell prompt open for the next task.

### Task 2: Use DateTime variables

1. To set the `$today` variable equal to today's date, at the Windows PowerShell prompt, enter the following command, and then press the Enter key:

   ```powershell
   $today = Get-Date
   ```

1. To review the variable type of the `$today` variable, enter the following command, and then press the Enter key:

   ```powershell
   $today.GetType()
   ```

1. To review the properties and methods for the `$today` variable, enter the following command, and then press the Enter key:

   ```powershell
   $today | Get-Member
   ```

1. To set a log file name based on the date, enter the following command, and then press the Enter key:

   ```powershell
   $logFile = [string]$today.Year + "-" + $today.Month + "-" + $today.Day + "-" + $today.Hour + "-" + $today.Minute + ".txt"
   ```

1. To calculate a date **30** days before today, enter the following command, and then press the Enter key:

   ```powershell
   $cutOffDate = $today.AddDays(-30)
   ```

1. To review users that have signed in for the last 30 days, enter the following command, and then press the Enter key:

   ```powershell
   Get-ADUser -Properties LastLogonDate -Filter {LastLogonDate -gt $cutOffDate}
   ```

1. Leave the Windows PowerShell prompt open for the next exercise.

## Exercise 2: Using arrays

### Exercise scenario 2

Now that you've practiced using different types of variables, you want to work with arrays.

The main tasks for this exercise are:

1. Use an array to update the department for users.
1. Use a generic list.

### Task 1: Use an array to update the department for users

1. To query all users in the **Marketing** department, at the Windows PowerShell prompt, enter the following command, and then press the Enter key:

   ```powershell
   $mktgUsers = Get-ADUser -Filter {Department -eq "Marketing"} -Properties Department
   ```

1. To identify how many users are in the `$mktgUsers` variable, enter the following command, and then press the Enter key:

   ```powershell
   $mktgUsers.count
   ```

1. To review the first user in `$mktgUsers`, enter the following command, and then press the Enter key:

   ```powershell
   $mktgUsers[0]
   ```

1. To modify the department to **Business Development**, enter the following command, and then press the Enter key:

   ```powershell
   $mktgUsers | Set-ADUser -Department "Business Development"
   ```

1. To review the **Name** and **Department** of users in the `$mktgUsers` variable, enter the following command, and then press the Enter key:

   ```powershell
   $mktgUsers | Format-Table Name,Department
   ```

1. Review the output and verify that the Department values in the `$mktgUsers` variable haven't changed.

1. To query all users in the **Marketing** department, at the Windows PowerShell prompt, enter the following command, and then press the Enter key:

   ```powershell
   Get-ADUser -Filter {Department -eq "Marketing"}
   ```

1. To query all users in the **Business Development** department, enter the following command, and then press the Enter key:

   ```powershell
   Get-ADUser -Filter {Department -eq "Business Development"}
   ```

1. Leave the Windows PowerShell prompt open for the next task.

### Task 2: Use a generic list

> **Note:** `ArrayList` is deprecated in favor of the strongly typed generic `List[T]` collection. For new scripts, use `[System.Collections.Generic.List[string]]` instead.

1. To create a generic list of computer names, at the Windows PowerShell prompt, enter the following command, and then press the Enter key:

   ```powershell
   [System.Collections.Generic.List[string]]$computers="LON-SRV1","LON-SRV2","LON-DC1"
   ```

1. To verify that the `$computers` list is not fixed-size, enter the following command, and then press the Enter key:

   ```powershell
   $computers.IsFixedSize
   ```

1. To add a computer name to the `$computers` list, enter the following command, and then press the Enter key:

   ```powershell
   $computers.Add("LON-DC2")
   ```

1. To remove a computer name from the `$computers` list, enter the following command, and then press the Enter key:

   ```powershell
   $computers.Remove("LON-SRV2")
   ```

1. To review the items in the `$computers` list, enter the following command, and then press the Enter key:

   ```powershell
   $computers
   ```

1. Leave the Windows PowerShell prompt open for the next exercise.

## Exercise 3: Using hash tables

### Exercise scenario 3

After using variables and arrays, you plan to practice working with hash tables. You want to learn how working with hash tables differs from arrays and generic lists.

The main task for this exercise is:

- Use a hash table.

### Task 1: Use a hash table

1. To create a hash table containing names and email addresses, at the Windows PowerShell prompt, enter the following command, and then press the Enter key:

   ```powershell
   $mailList=@{"Frank"="Frank@fabriakm.com";"Libby"="LHayward@contso.com";"Matej"="MSTaojanov@tailspintoys.com"}
   ```

1. To review the contents of the `$mailList` hash table, enter the following command, and then press the Enter key:

   ```powershell
   $mailList
   ```

1. To review the email address for **Libby**, enter the following command, and then press the Enter key:

   ```powershell
   $mailList.Libby
   ```

1. To update the email address for **Libby**, enter the following command, and then press the Enter key:

   ```powershell
   $mailList.Libby="Libby.Hayward@contoso.com"
   ```

1. To add a new name and email address to the hash table, enter the following command, and then press the Enter key:

   ```powershell
   $mailList.Add("Stela","Stela.Sahiti")
   ```

1. To remove **Frank** from the hash table, enter the following command, and then press the Enter key:

   ```powershell
   $mailList.Remove("Frank")
   ```

1. To review the contents of the `$mailList` hash table, enter the following command, and then press the Enter key:

   ```powershell
   $mailList
   ```

1. Close the Windows PowerShell prompt.
