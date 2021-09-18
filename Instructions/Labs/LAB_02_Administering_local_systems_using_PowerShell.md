---
lab:
    title: 'Lab: Performing local system administration with PowerShell'
    module: 'Module 2: Windows PowerShell for local systems administration'
---

# Lab: Performing local system administration with PowerShell

## Scenario

You work for Adatum Corporation on the server support team. One of your first assignments is to configure the infrastructure service for a new branch office. You decide to complete the tasks by using Windows PowerShell.

## Objectives

After completing this lab, you'll be able to:

- Create and manage Active Directory objects by using Windows PowerShell.
- Configure network settings on Windows Server by using Windows PowerShell.
- Create an IIS website by using Windows PowerShell.

## Estimated time: 60 minutes

## Lab setup

Virtual machines: **AZ-040T00A-LON-DC1**, **AZ-040T00A-LON-SVR1**, and **AZ-040T00A-LON-CL1**

Username: **Adatum\\Administrator**

Password: **Pa55w.rd**

## Lab Startup

1. Select **LON-DC1**.
1. Sign in by using the following credentials:

   - Username: **Administrator**
   - Password: **Pa55w.rd**
   - Domain: **Adatum**

1. Repeat these steps for **LON-CL1** and **LON-SVR1**.

## Exercise 1: Creating and managing Active Directory objects

### Exercise scenario 1

In this exercise, you'll create and manage Active Directory objects to create an organizational unit (OU) for a branch office, along with groups for OU administrators. You'll create accounts for a user and computer in the branch office, in the default OU, and add the user to the administrators group. You'll later move the user and computer to the OU that you created for the branch office. You'll use individual Windows PowerShell commands to accomplish these tasks from a client computer.

The main tasks for this exercise are:

1. Create a new OU for a branch office.
1. Create a group for branch office administrators.
1. Create a user and computer account for the branch office.
1. Move the group, user, and computer accounts to the branch office OU.

### Task 1: Create a new OU for a branch office

- From **LON-CL1**, use Windows PowerShell to create a new OU named **London**.

### Task 2: Create a group for branch office administrators

- In the **PowerShell** console, create the **London Admins** global security group.

### Task 3: Create a user and computer account for the branch office

1. In the **PowerShell** console, create a user account for the user **Ty Carlson**.
2. Add the user to the **London Admins** group.
3. Create a computer account for the **LON-CL2** computer.

### Task 4: Move the group, user, and computer accounts to the branch office OU

- Use Windows PowerShell to move the following group, user, and computer accounts to the London OU:

  - **London Admins**
  - **Ty Carlson**
  - **LON-CL2**

### Exercise 1 results

After completing this exercise, you'll have successfully identified and used commands for managing Active Directory objects in the Windows PowerShell command-line interface.

## Exercise 2: Configuring network settings on Windows Server

### Exercise scenario 2

In this exercise, you'll configure network settings on Windows Server. To review the effect, you'll test network connectivity before and after making changes. You'll use individual Windows PowerShell commands to accomplish these tasks on the server.

The main tasks for this exercise are:

1. Test the network connection and review the configuration.
1. Change the server IP address.
1. Change the DNS settings and default gateway for the server.
1. Verify and test the changes.

### Task 1: Test the network connection and review the configuration

1. Switch to **LON-SVR1**.
2. Open **Windows PowerShell** with administrative permissions.
3. Test the connection to **LON-DC1** and note the speed of the test.
4. Review the network configuration for **LON-SVR1**.
5. Note the IP address, default gateway, and DNS server.

### Task 2: Change the server IP address

- Use Windows PowerShell to change the IP address for the **Ethernet** network interface to **172.16.0.15/16**.

### Task 3: Change the DNS settings and default gateway for the server

1. Change the DNS settings of the **Ethernet** network interface to point at **172.16.0.12**.
2. Change the default gateway for the **Ethernet** network interface to **172.16.0.2**.

### Task 4: Verify and test the changes

1. On **LON-SVR1**, verify the changes to the network configuration.
2. Test the connection to **LON-DC1**, and then note the difference in the test speed.

### Exercise 2 results

After completing this exercise, you'll have successfully identified and used Windows PowerShell commands for managing network configuration.

## Exercise 3: Creating a website

### Exercise scenario 3

In this exercise, you'll install the Web Server (IIS) server role and create a new internal website for the London branch. You'll use individual Windows PowerShell commands to accomplish these tasks on the server.

The main tasks for this exercise are:

1. Install the Web Server (IIS) role on the server.
1. Create a folder on the server for the website files.
1. Create the IIS website.

### Task 1: Install the Web Server (IIS) role on the server

- On **LON-SVR1**, use Windows PowerShell to install the Web server (IIS) role on **LON-SVR1**.

### Task 2: Create a folder on the server for the website files

- On **LON-SVR1**, use PowerShell to create a folder named **London** under **C:\inetpub\wwwroot** for the website files.

### Task 3: Create the IIS website

1. On **LON-SVR1**, use PowerShell to create the IIS website by using the following configuration:

    - Name: **London**
    - Physical path: The folder that you previously created
    - Binding information: The current IP address of **LON-SVR1** using port **8080**

1. Open the website in Internet Explorer by using the IP address and port **8080**, and then verify that the site is using the provided settings. Internet Explorer will display an error message that a document hasn't been configured for the URL. The error message details give the physical path of the site, which should be **C:\\inetpub\\wwwroot\\london**.

### Exercise 3 results

After completing this exercise, you'll have successfully identified and used Windows PowerShell commands that would be used as part of a standardized web server configuration.
