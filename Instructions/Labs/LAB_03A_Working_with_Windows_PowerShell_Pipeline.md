---
lab:
    title: 'Lab A: Using PowerShell pipeline'
    module: 'Module 3: Working with the Windows PowerShell pipeline'
---

# Lab: Using PowerShell pipeline

## Scenario

One of your administrative tasks at Adatum Corporation is to configure advanced PowerShell scripts. You need to ensure that you understand the foundations of working with PowerShell pipeline by sorting, filtering, enumerating, and converting objects.

## Objectives

After completing this lab, you'll be able to:

- Select, sort, and display data by using pipelines.
- Filter objects out of the pipeline by using basic and advanced syntax forms.

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

## Exercise 1: Selecting, sorting, and displaying data

### Exercise scenario 1

In this exercise, you'll produce lists of management information from the computers in your environment. For each task, you'll discover the necessary commands and use **Select-Object**, **Sort‑Object,** and the formatting cmdlets to customize the final output of each command.

The main tasks for this exercise are:

1. Display the current day of the year.
1. Display information about installed hotfixes.
1. Display a list of available scopes from the DHCP server.
1. Display a sorted list of enabled Windows Firewall rules.
1. Display a sorted list of network neighbors.
1. Display information from the DNS name resolution cache.

### Task 1: Display the current day of the year

1. On **LON-CL1**, start Windows PowerShell with administrative credentials.
2. Using a keyword such as **date**, find a command that can display the current date.
3. Display the members of the object produced by the command that you found in the previous step.
4. Display only the day of the year.
5. Display the results of the previous command on a single line.

### Task 2: Display information about installed hotfixes

1. Using a keyword such as **hotfix**, find a command that can display a list of the installed hotfixes.
1. Display the members of the object produced by the command that you found in the previous step.
1. Display a list of the installed hotfixes. Display only the installation date, hotfix ID number, and name of the user who installed the hotfix.
1. Display a list of the installed hotfixes. Display only the hotfix ID, the number of days since the hotfix was installed, and the name of the user who installed the hotfix.

### Task 3: Display a list of available scopes from the DHCP server

1. Using a keyword such as **DHCP** or **scope**, find a command that can display a list of Internet Protocol version 4 (IPv4) Dynamic Host Configuration Protocol (DHCP) scopes.
1. Review the help for the command.
1. Display a list of the available IPv4 DHCP scopes on **LON-DC1**.
1. Display a list of the available IPv4 DHCP scopes on **LON-DC1**. This time, include only the scope ID, subnet mask, and scope name, and display the data in a single column.

### Task 4: Display a sorted list of enabled Windows Firewall rules

1. Using a keyword such as **rule**, find a command that can display the firewall rules.
1. Display a list of the firewall rules.
1. Review the help for the command that displays the firewall rules.
1. Display a list of the firewall rules that are enabled.
1. Display the same data in a table, making sure no information is truncated.
1. Display a list of the enabled firewall rules. Display only the rules’ display names, the profiles they belong to, their directions, and whether they allow or deny access.
1. Sort the list in alphabetical order first by profile and then by display name, with the results displaying in a separate table for each profile.

### Task 5: Display a sorted list of network neighbors

1. Using a keyword such as **neighbor**, find a command that can display the network neighbors.
1. Review the help for the command.
1. Display a list of the network neighbors.
1. Display a list of the network neighbors that's sorted by state.
1. Display a list of the network neighbors that's grouped by state, displaying only the IP address in as compact a format as possible and letting Windows PowerShell decide how to optimize the layout.

### Task 6: Display information from the DNS name resolution cache

1. Test your network connection to both **LON-DC1** and **LON-CL1** so that you know the Domain Name System (DNS) client cache is populated with data.
1. Using a keyword such as **cache**, find a command that can display items from the DNS client cache.
1. Display the DNS client cache.
1. Display the DNS client cache. Sort the list by record name, and display only the record name, record type, and Time to Live. Use only one column to display all the data.

### Exercise 1 results

After completing this exercise, you should have produced several custom reports that contain management information from your environment.

## Exercise 2: Filtering objects

### Exercise scenario 2

In this exercise, you'll use filtering to produce lists of management information that include only specified data and elements for the reports you must produce.

The main tasks for this exercise are:

1. Display a list of all the users in the Users container of Active Directory.
1. Create a report displaying the Security event log entries that have the event ID **4624**.
1. Display a list of the encryption certificates installed on the computer.
1. Create a report that displays the disk volumes that are running low on space.
1. Create a report that displays specified Control Panel items.

### Task 1: Display a list of all the users in the Users container of Active Directory

1. On **LON-CL1**, open **Windows PowerShell** as an administrator.
1. Using a keyword such as **user,** find a command that can list Active Directory users.
1. Review the help for the command and identify any mandatory parameters.
1. Display a list of all the users in Active Directory in a format that lets you easily compare properties.
1. Display the same list of all the users in the same format. This time, however, display only those users in the **Users** container of Active Directory. Use a search base of **"cn=Users,dc=adatum,dc=com"** for this task.

### Task 2: Create a report displaying the Security event log entries that have the event ID 4624

1. Display only the total number of **Security** event log entries that have the event ID **4624**.
1. Display the full list of the **Security** event log entries that have the event ID **4624**, and display only the time written, event ID, and message.
1. Display only the 10 oldest entries in a format that lets you review the message details.

### Task 3: Display a list of the encryption certificates installed on the computer

1. Display a directory listing of all the items on the **CERT** drive. Include subfolders in the list.
1. Display the list again and display the name and issuer for only the certificates that don't have a private key. Display the results in one column.
1. Display the list again and display only the current certificates. Those certificates have a **NotBefore** date that's before today and a **NotAfter** date that's after today. Include the **NotBefore** and **NotAfter** properties in the results and display the results in a format that allows you to easily compare dates. Also, make sure that no data is truncated.

### Task 4: Create a report that displays the disk volumes that are running low on space

1. Display a list of the disk volumes.
1. Display a list in one column of the volumes that have more than zero bytes of free space.
1. Display a list of the volumes that have less than 99 percent free space and more than zero bytes of free space. Display only the drive letter and disk size, in megabytes (MB).
1. Display a list of the volumes that have less than 10 percent free space and more than zero bytes of free space. This command might produce no results if no volumes on your computer meet the criteria.

   > **Note:** This command might not produce any output on your lab computer if the computer has more than 10 percent free space on each of its volumes.

### Task 5: Create a report that displays specified Control Panel items

1. Display a list of all the Control Panel items.
1. Display the names and descriptions, sorted by name, of the Control Panel items in the **System and Security** category.
1. Display the same list, excluding any Control Panel items that exist in more than one category. Make sure the command performance is optimized.

### Exercise 2 results

After completing this exercise, you should have used filtering to produce lists of management information that include only specified data and elements.
