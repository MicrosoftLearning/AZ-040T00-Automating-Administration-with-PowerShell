---
lab:
    title: 'Lab B: Using PowerShell pipeline'
    module: 'Module 3: Working with the Windows PowerShell pipeline'
---

# Lab: Using PowerShell pipeline

## Scenario

One of your administrative tasks at Adatum Corporation is to configure advanced PowerShell scripts. You need to ensure that you understand the foundations of working with PowerShell pipeline by sorting, filtering, enumerating, and converting objects.

## Objectives

After completing this lab, you'll be able to:

- Enumerate pipeline objects by using basic and advanced syntax.
- Convert objects to different formats.

## Estimated Time: 60 minutes

## Lab setup

Virtual machines: **AZ-040T00A-LON-DC1**, **AZ-040T00A-LON-SVR1**, and **AZ-040T00A-LON-CL1**

Username: **Adatum\\Administrator**

Password: **Pa55w.rd**

## Lab startup

1. Select **LON-DC1**.
1. Sign in by using the following credentials:
   - Username: **Administrator**
   - Password: **Pa55w.rd**
   - Domain: **Adatum**

1. Repeat these steps for **LON-CL1** and **LON-SVR1**.

## Exercise 1: Enumerating objects

### Exercise scenario 1

In this exercise, you'll create commands that manipulate multiple objects in the pipeline. In some tasks, you need to use enumeration. In other tasks, you'll not need to use enumeration. Decide the best approach for each task.

The main tasks for this exercise are:

1. Display a list of files on drive **E** of your computer.
1. Use enumeration to produce 100 random numbers.
1. Run a method of a Windows Management Instrumentation (WMI) object.

### Task 1: Display a list of files on drive E of your computer

1. On **LON-CL1**, start Windows PowerShell with administrative credentials.
1. Display a directory listing of all the items on drive **E**. Include subfolders in the list.
1. Display a list of all the files on drive **E**, without displaying directory names.

### Task 2: Use enumeration to produce 100 random numbers

1. Using a keyword such as **random**, find a command that produces random numbers.
1. Review the help for the command.
1. Run **1..100** to put 100 numeric objects into the pipeline.
1. Run the command again. For each numeric object, produce a random number that uses the numeric object as the seed.

### Task 3: Run a method of a Windows Management Instrumentation (WMI) object

1. Close all applications other than the **Windows PowerShell console**.
1. Run the command **Get-WmiObject -Class Win32_OperatingSystem -EnableAllPrivileges**.
1. Display the members of the object produced by the previous command.
1. In the member list, find a method that restarts the computer.
1. Run the command again and use enumeration to run the method that restarts the computer.

   > **Note:** The command will restart the machine you run it on.

### Exercise 1 results

After completing this exercise, you should have created commands that manipulate multiple objects in the pipeline.

## Exercise 2: Converting objects

### Exercise scenario 2

In this exercise, you'll create commands that query Active Directory users and make changes to information about them. You'll also create commands that store the user data in various file formats. Then, you'll review the files to determine which data format you think is the most useful.

The main tasks for this exercise are:

1. Update Active Directory user information.
1. Generate files listing the Active Directory users in the IT department.

### Task 1: Update Active Directory user information

1. Sign in to the **LON-CL1** as **Adatum\\Administrator** with the password **Pa55w.rd**.
1. Start **Windows PowerShell** as an administrator.
1. Display the name, department, and city for all the users in the IT department who are located in London, in alphabetical order by name.
1. Set the **Office** location for all the users to **LON-A/1000**.
1. Display the list of users again, including the office assignment for each user.

### Task 2: Generate files listing the Active Directory users in the IT department

1. Review the help for **ConvertTo-Html**.
1. Display the same list again, and then convert the list to an HTML page. Store the HTML data in **E:\\UserReport.html**. Have the word **Users** display before the list of users.
1. Use Internet Explorer to review **UserReport.html**.
1. Display the same list again, and then convert it to XML.
1. Use Internet Explorer to review **UserReport.xml**.
1. Display a list of all the properties of all the Active Directory users in a comma-separated value (CSV) file.
1. Open the CSV file in Notepad.
1. Open the CSV file in Microsoft Excel.

### Exercise 2 results

After completing this exercise, you should have queried Active Directory users, made changes to information about them, as well as converted Active Directory user objects to different data formats.
