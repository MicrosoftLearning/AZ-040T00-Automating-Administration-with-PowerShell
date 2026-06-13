---
lab:
  title: 'Lab: Jobs management with PowerShell'
  type: Answer Key
  module: 'Module 11: Using background jobs and scheduled jobs'
  description: Create and manage PowerShell background and scheduled jobs for asynchronous automation. You monitor job execution and configure recurring tasks for repeatable administration.
  duration: 15 minutes
  level: 200
  islab: true
  primarytopics:
    - Background Jobs
    - Scheduled Jobs
    - Automation
---

# Jobs management with PowerShell

This lab should take approximately **15** minutes to complete.

## Scenario

Background jobs provide a useful way to run multiple commands simultaneously and long-running commands in the background. In this lab, you'll learn to create and manage two of the three basic kinds of jobs.

You'll create and configure two scheduled jobs. You'll also create a scheduled task using a Windows PowerShell script that searches for and removes disabled accounts from a certain security group.

## Objectives

After completing this lab, you'll be able to:

- Start and manage jobs.
- Create a scheduled job.

## Lab setup

Virtual machines: **LON-DC1**, **LON-SVR1**, and **LON-CL1**

Username: **Adatum\\Administrator**

Password: **Pa55w.rd**

For this lab, you'll use the available virtual machine (VM) environment. Before you begin the lab, complete the following steps:

1. Open **LON-DC1** and sign in as **Adatum\\Administrator** with the password **Pa55w.rd**.
1. Repeat step 1 for **LON-SVR1** and **LON-CL1**.

## Exercise 1: Starting and managing jobs

### Exercise scenario 1

In this exercise, you'll start jobs using two of the basic job types.

The main tasks for this exercise are:

1. Start a Windows PowerShell remote job.
1. Start a local job.
1. Review and manage job status.

### Task 1: Start a Windows PowerShell remote job

1. Ensure that you're signed into **LON-CL1** as **Adatum\\Administrator** with the password **Pa55w.rd**.
1. Select **Start**, and then enter **powersh**.
1. In the results list, right-click **Windows PowerShell** or activate its context menu, and then select **Run as administrator**.
1. To start a Windows PowerShell remote job that retrieves a list of physical network adapters from **LON-DC1** and **LON-SVR1**, enter the following command, and then press the Enter key:

   ```powershell
   Invoke-Command –ScriptBlock { Get-NetAdapter –Physical } –ComputerName LON-DC1,LON-SVR1 –AsJob –JobName RemoteNetAdapt
   ```

1. To start a Windows PowerShell remote job that retrieves a list of Server Message Block (SMB) shares from **LON-DC1** and **LON-SVR1**, enter the following command, and then press the Enter key:

   ```powershell
   Invoke-Command –ScriptBlock { Get-SMBShare } –ComputerName LON-DC1,LON-SVR1 –AsJob –JobName RemoteShares
   ```

1. To start a Windows PowerShell remote job that retrieves all instances of the **Win32_Volume** class from every computer in Active Directory Domain Services (AD DS), enter the following commands, and then press the Enter key after each:

   ```powershell
   Enable-PSRemoting –SkipNetworkProfileCheck –Force
   Invoke-Command –ScriptBlock { Get-CimInstance –ClassName Win32_Volume } –ComputerName (Get-ADComputer –Filter * | Select –Expand Name) –AsJob –JobName RemoteDisks
   ```

> **Note:** You need to enable PowerShell Remoting on LON-CL1 in order to connect to it by using PowerShell Remoting, which is, by default, disabled on Windows 10. The **RemoteDisk** targets all domain computers, including LON-CL1.

> **Note:** Because some of the computers in the domain might not be online, this job might not complete successfully. This is expected behavior.

### Task 2: Start a local job

1. To start a local job that retrieves all entries from the Security event log, enter the following command, and then press the Enter key:

   ```powershell
   Start-Job –ScriptBlock { Get-EventLog –LogName Security } –Name LocalSecurity
   ```

   > **Note:** `Get-EventLog` is only available in Windows PowerShell 5.1. In PowerShell 7, use `Start-Job -ScriptBlock { Get-WinEvent -LogName Security } -Name LocalSecurity` instead.

1. To start a local job that produces 100 directory listings, enter the following command, and then press the Enter key:

   ```powershell
   Start-Job –ScriptBlock { 1..100 | ForEach-Object { Dir C:\ -Recurse } } –Name LocalDir
   ```

> **Note:** This job will take a long time to complete. Don't wait for it to complete. Proceed to the next task.

### Task 3: Review and manage job status

1. Ensure that you're signed in to **LON-CL1** as **Adatum\\Administrator** with the password **Pa55w.rd**.
1. To display a list of running jobs, enter the following command, and then press the Enter key:

   ```powershell
   Get-Job
   ```

1. To display a list of running jobs whose names start with **remote**, enter the following command, and then press the Enter key:

   ```powershell
   Get-Job –Name Remote*
   ```

1. To stop the **LocalDir** job, enter the following command, and then press the Enter key:

   ```powershell
   Stop-Job –Name LocalDir
   ```

1. Run **Get-Job** until there are no jobs with the status of **Running**.
1. To receive the results of the **RemoteNetAdapt** job, enter the following command, and then press the Enter key:

   ```powershell
   Receive-Job –Name RemoteNetAdapt
   ```

1. To receive the results of the **RemoteDisks** job from **LON-DC1** only, enter the following command, and then press the Enter key:

   ```powershell
   Get-Job -Name RemoteDisks | 
     Select-Object -ExpandProperty ChildJobs | 
     Where-Object { $_.Location -eq 'LON-DC1' } | 
     Receive-Job
   ```

## Exercise 2: Creating a scheduled job

> **Note:** The `Register-ScheduledJob` cmdlet and the **PSScheduledJob** module are only available in Windows PowerShell 5.1. Ensure you are running this exercise in a Windows PowerShell 5.1 console, not PowerShell 7.

### Exercise scenario 2

In this exercise, you'll create and run a scheduled job and retrieve its results. You'll then create and run a scheduled task from a Windows PowerShell script that removes a disabled user from a security group in AD DS.

The main tasks for this exercise are:

1. Create job options and job triggers.
1. Create a scheduled job and retrieve results.
1. Use a Windows PowerShell script as a scheduled task.

### Task 1: Create job options and a job trigger

1. Ensure that you're signed in to **LON-CL1** as **Adatum\\Administrator** with the password **Pa55w.rd**.
1. To create a new job option, enter the following command, and then press the Enter key:

   ```powershell
   $option = New-ScheduledJobOption –WakeToRun -RunElevated
   ```

1. To create a new job trigger, enter the following command, and then press the Enter key:

   ```powershell
   $trigger1 = New-JobTrigger –Once –At (Get-Date).AddMinutes(5)
   ```

### Task 2: Create a scheduled job and retrieve results

1. To register the job, enter the following command, and then press the Enter key:

   ```powershell
   Register-ScheduledJob –ScheduledJobOption $option `
   –Trigger $trigger1 `
   –ScriptBlock { Get-EventLog –LogName Security } `
   –Name LocalSecurityLog
   ```

1. To display a list of job triggers, enter the following command, and then press the Enter key:

   ```powershell
   Get-ScheduledJob –Name LocalSecurityLog | 
   Select –Expand JobTriggers 
   ```

1. Note the time that displays, and then wait until the time returned in the output of step 2 has passed.
1. To display a list of jobs, enter the following command, and then press the Enter key:

   ```powershell
   Get-Job
   ```

1. To receive the job results, wait until 5 minutes passed from the time you registered the **LocalSecurityLog** job, then enter the following command, and press the Enter key:

   ```powershell
   Receive-Job –Name LocalSecurityLog
   ```

> **Note:** Verify that the output consists of a list of log entries.

### Task 3: Use a Windows PowerShell script as a scheduled task

1. Switch to the console session to **LON-DC1** and, if needed, sign into **LON-DC1** as **Adatum\\Administrator** with the password **Pa55w.rd**.
1. On **LON-DC1**, in **Server Manager**, select **Tools**, and then select **Active Directory Users and Computers**.
1. In the **Active Directory Users and Computers** console tree, select and expand **Adatum.com**, and then select **Managers**.
1. In the details pane of **Managers**, select one of the user accounts, such as **Adam Hobbs**. Right-click the account or activate its context menu, and then select **Disable Account**. 
1. Double-click the user you disabled, or select it and then press the Enter key.
1. Select the **Member of** tab and verify that the user is a member of the Managers security group.
1. Select **OK** and then minimize **Active Directory Users and Computers**.
1. Select **Start**, enter **Task Scheduler**, and then select **Task Scheduler**.
1. In **Task Scheduler**, in the console tree, right-click **Task Scheduler (local)** or activate its context menu, and then select **Create Task**.
1. In the **Create Task** window, in the **General** tab, in the **Name** and **Description** boxes, enter **Remove Disabled User from Managers Security Group**. 
1. In the **Security options** section, select **Run whether user is logged on or not**, and then select the **Run with highest privileges** checkbox.
1. In the **Triggers** tab, select **New**.
1. In the **New Trigger** window, in **Settings**, select **Daily**, in the **Start time** box, change the time to 5 minutes from the current time, and then select **OK**.

   > **Note:** If you get a **Task Scheduler** pop-up window, select **OK**.

1. In the **Actions** tab, select **New**.
1. In the **New Action** window, in the **Program/script** box, enter **PowerShell.exe**.
1. In the **Add arguments (optional)** box, enter **-ExecutionPolicy Bypass E:\\Labfiles\\\Mod11\\DeleteDisabledUserManagersGroup.ps1**, select **OK** and then, in a pop-up window, select **Yes**.
1. In the **Conditions** tab, review the items, but make no changes.
1. In the **Settings** tab, in the **If the task is already running, then the following rule applies:** drop-down list, select **Stop the existing instance**, and then select **OK**.
1. In the **Task Scheduler** credentials pop-up window, in the **Password** box, enter **Pa55w.rd**, and then select **OK**.
1. In **Task Scheduler**, select **Task Schedule Library** and then in the details pane, select **Remove Disabled User from Managers Security Group**.
1. In the details pane, select the **History** tab. After the five minutes pass, select **Refresh** in the **Actions** pane. You should notice an item with the **Task Category** of **Task completed**.
1. Maximize **Active Directory Users and Computers**.
1. Double-click the user you disabled, or select it and then press the Enter key.
1. Select the **Member of** tab. The user should no longer be a member of the Managers security group.
