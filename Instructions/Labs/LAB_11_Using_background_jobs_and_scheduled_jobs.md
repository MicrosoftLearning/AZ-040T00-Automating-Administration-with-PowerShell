---
lab:
    title: 'Lab: Jobs management with PowerShell'
    module: 'Module 11: Using background jobs and scheduled jobs'
---

# Lab: Jobs management with PowerShell

## Scenario

Background jobs provide a useful way to run multiple commands simultaneously and long-running commands in the background. In this lab, you'll learn to create and manage two of the three basic kinds of jobs.

You'll create and configure two scheduled jobs. You'll also create a scheduled task using a Windows PowerShell script that searches for and removes disabled accounts from a certain security group.

## Objectives

After completing this lab, you'll be able to:

- Start and manage jobs.
- Create a scheduled job.

### Estimated time: 30 minutes

## Lab Setup

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

1. Start a Windows PowerShell job.
1. Start a local job.
1. Review and manage job status.

### Task 1: Start a Windows PowerShell job

1. Ensure that you're signed in to **LON-CL1** as **Adatum\\Administrator** with the password **Pa55w.rd**.
1. Start a Windows PowerShell remoting job that retrieves a list of physical network adapters from **LON-DC1** and **LON-SVR1**. Name the job **RemoteNetAdapt**.
1. Start a Windows PowerShell remote job that retrieves a list of Server Message Block (SMB) shares from **LON-DC1** and **LON-SVR1**. Name the job **RemoteShares**.
1. Start a Windows PowerShell remote job that retrieves all instances of the **Win32_Volume** Common Information Model (CIM) class from every computer in Active Directory Domain Services (AD DS). Name the job **RemoteDisks**. Because some domain computers might not start, some child jobs might fail.

### Task 2: Start a local job

1. Start a local job that retrieves all entries from the **Security** event log. Name the job **LocalSecurity**.
1. Using the range operator (**..**) and **ForEach-Object**, start a local job that produces 100 directory listings of drive C, including subfolders. Name the job **LocalDir**. Proceed to the next task while this job is still running.

### Task 3: Review and manage job status

1. Ensure that you're signed in to **LON-CL1** as **Adatum\\Administrator** with the password **Pa55w.rd**.
1. Display a list of running jobs.
1. Display a list of running jobs whose names start with **remote**.
1. Force the **LocalDir** job to stop.
1. Wait for all remaining jobs to finish successfully or fail.
1. Receive the results of the **RemoteNetAdapt** job.
1. Use a single command line to receive the results from **LON-DC1** for the **RemoteDisks** job.

> **Note:** You must start by querying the parent job, and then expanding its **ChildJob** property. Filter the child jobs so that just the **LON-DC1** job remains, and then receive the results from that job. You'll use a total of four commands to complete this step.

## Exercise 2: Creating a scheduled job

### Exercise scenario 2

In this exercise, you'll create and run a scheduled job and retrieve its results. You'll then create and run a scheduled task from a Windows PowerShell script that removes a disabled user from a security group in AD DS.

The main tasks for this exercise are:

1. Create job options and job triggers.
1. Create a scheduled job and retrieve results.
1. Use a Windows PowerShell script as a scheduled task.

### Task 1: Create job options and job triggers

1. Ensure that you're signed into **LON-CL1** as **Adatum\\Administrator** with the password **Pa55w.rd**.
1. Create a job option object and store it in `$option`. Configure the job object so the job will:

    - Wake the computer to run.
    - Run under elevated permissions.

1. Create a job trigger object and store it in `$trigger1`. Configure the trigger so the job will:

    - Run once in five minutes. Use **Get-Date** and a method of the resulting **DateTime** object to calculate five minutes from now.

### Task 2: Create a scheduled job and retrieve results

1. Using `$option` and `$trigger1`, create a new scheduled job that has the following attributes:

    - The job action retrieves all entries from the **Security** event log.
    - The job name is **LocalSecurityLog**.
    - The maximum number of job results is five.

1. Display a list of job triggers, including time, for the **LocalSecurityLog** scheduled job.
1. Wait until the time displayed in step 2 has passed.
1. Display a list of jobs.
1. Receive the job results for **LocalSecurityLog**.

### Task 3: Use a Windows PowerShell script as a scheduled task

1. On **LON-DC1**, open **Active Directory Users and Computers**.
1. Select a user from the **Managers** organizational unit (OU) in **Active Directory Users and Computers**, and then disable the user account.
1. Open the **Task Scheduler**.
1. Create a new task with the following properties:

    - Name and description: **Delete Disabled User from Managers Security Group**
    - Security options: **Run whether user is logged on or not** and **Run with highest privileges**
    - Trigger settings: **Daily** and set the time to five minutes after the current time
    - Actions: Set **Program/script** to **PowerShell.exe**
    - Add arguments (optional): Enter **-ExecutionPolicy Bypass E:\\Labfiles\\Mod11\\DeleteDisabledUserManagersGroup.ps1**
    - Settings: Set **If the task is already running, then the following rule applies** to **Stop the existing instance**

1. After five minutes, review the history of the **Delete Disabled User from Managers Security Group** task.
1. Return to **Active Directory Users and Computers** and verify that the disabled user account from step 2 is no longer a member of the **Managers** security group.
