---
lab:
    title: 'Lab: Performing remote administration with PowerShell'
    module: 'Module 8: Administering remote computers with Windows PowerShell'
---

# Lab: Performing remote administration with PowerShell

## Scenario

You're an administrator for Adatum Corporation and must perform maintenance tasks on a server running Windows Server 2019. You don't have physical access to the server, and instead plan to perform the tasks using Windows PowerShell remoting. You also have some tasks to perform on both a server and another client computer that runs Windows 10. In your environment, communication protocols such as remote procedure call (RPC) are blocked between your local computer and the servers. You plan to use Windows PowerShell remoting, and want to use sessions to provide persistence and reduce the setup and cleanup overhead that improvised remoting connections will impose.

## Objectives

After completing this lab, you'll be able to:

- Enable remoting on a client computer.
- Run a task on a remote computer by using one-to-one remoting.
- Run a task on two computers by using one-to-many remoting.
- Create and manage PSSessions.
- Send commands to multiple computers in parallel.

## Estimated time: 60 minutes

## Lab Setup

Virtual machines:

- **LON-DC1**
- **LON-CL1**

Username: **Adatum\\Administrator**

Password: **Pa55w.rd**

For this lab, you'll use the available virtual machine environment. Before you begin the lab, complete the following steps:

1. Open **LON-DC1**, and then sign in as **Administrator** with the password **Pa55w.rd**.
1. Repeat step 1 for **LON-CL1**.

## Exercise 1: Enabling remoting on the local computer

### Scenario 1

In this exercise, you'll enable remoting on the client computer.

The main task for this exercise is:

- Enable remoting for incoming connections.

### Task 1: Enable remoting for incoming connections

1. Ensure that you're signed in to **LON-CL1** as **Adatum\\Administrator**.
1. Ensure the Windows PowerShell command window is open.
1. Ensure that **ExecutionPolicy** is set to **RemoteSigned**.
1. Enable remoting for incoming connections on the **LON-CL1** client computer.
1. Verify that Windows PowerShell has created several session configurations. You have to find a command that can produce this list.

## Exercise 2: Performing one-to-one remoting

### Scenario 2

In this exercise, you'll connect to a remote computer and perform maintenance tasks.

The main tasks for this exercise are:

1. Connect to the remote computer and install an operating system feature on it.
1. Test multi-hop remoting.
1. Observe remoting limitations.

### Task 1: Connect to the remote computer and install an operating system feature on it

1. Ensure that you're still signed in to **LON-CL1**.
1. On **LON-CL1**, in the Windows PowerShell console, use remoting to establish a one-to-one connection to **LON-DC1**.
1. Install the Network Load Balancing (NLB) feature on **LON-DC1**.
1. Disconnect from **LON-DC1**.

### Task 2: Test multi-hop remoting

1. Establish a one-to-one remoting connection with **LON-DC1**.
1. Try to establish a connection from **LON-DC1** to **LON-CL1**. What happens and why?
1. Close the connection.

### Task 3: Observe remoting limitations

1. Establish a one-to-one remoting connection to **LON-CL1** using the computer name **localhost**. This is your local computer, but this new connection creates a second user session for you on the computer.
1. Use Windows PowerShell to start a new instance of Notepad. What happens, and why?
1. Stop the pipeline to exit the Notepad process.
1. Close the connection.

## Exercise 3: Performing one-to-many remoting

In this exercise, you'll run commands against multiple computers. One of those will be the client computer, although you'll be establishing a second sign-in to it for the duration of each command.

The main tasks for this exercise are:

1. Retrieve a list of physical network adapters from two computers.
1. Compare the output of a local command to that of a remote command.

### Task 1: Retrieve a list of physical network adapters from two computers

1. On **LON-CL1**, using a keyword such as **adapter**, find a command that can list network adapters.
1. Review the Help for the command, then find a switch parameter that will limit output to physical adapters.
1. Use remoting to run the command on both **LON-CL1** and **LON-DC1**.

### Task 2: Compare the output of a local command to that of a remote command

1. Pipe a collection of **Process** objects to **Get-Member**.
2. Use remoting to retrieve a list of **Process** objects from **LON-DC1**, and then pipe them to **Get-Member**.
3. Compare the output of the two **Get-Member** results.

## Exercise 4: Using implicit remoting

In this exercise, you'll use implicit remoting to import and run commands from a remote computer.

The main tasks for this exercise are as follows:

1. Create a persistent remoting connection to a server.
1. Import and use a module from a server.
1. Close all open remoting connections.

### Task 1: Create a persistent remoting connection to a server

1. On **LON-CL1**, sign in as **Adatum\\Administrator** with the password **Pa55w.rd**.
2. Select the **Start** menu, and then enter **powersh**.
3. In the results list, right-click **Windows PowerShell** or activate its context menu, and then select **Run as administrator**.
4. In the Windows PowerShell command window, create a persistent remoting connection to **LON-DC1**, and then save the resulting PSSession object in the variable `$dc`.
5. Display a list of PSSessions in `$dc` and verify their availability.

### Task 2: Import and use a module from a server

1. From **LON-CL1**, display a list of Windows PowerShell modules on **LON-DC1**.
1. Locate a module on **LON-DC1** that can work with Server Message Block (SMB) shares.
1. Import the module to your local computer, and then add the prefix **DC** to the nouns for each imported command.
1. Display a list of SMB shares on **LON-DC1**.
1. Display a list of SMB shares on the client computer.

### Task 3: Close all open remoting connections

- In the Windows PowerShell console, close all open remoting connections.

## Exercise 5: Managing multiple computers

In this exercise, you'll perform several management tasks against multiple computers, relying on PSSessions to provide persistence.

The main tasks for this exercise are:

1. Create PSSessions to two computers.
1. Create a report that displays Windows Firewall rules from two computers.
1. Create and display an HTML report that displays local disk information from two computers.
1. Close all open PSSessions.

### Task 1: Create PSSessions to two computers

1. In the **Windows PowerShell** console, create PSSessions to both **LON-CL1** and **LON-DC1**.
1. Save both PSSession objects in the variable `$computers`.
1. Verify that the connections in `$computers are open and available.

### Task 2: Create a report that displays Windows Firewall rules from two computers

1. Find a Windows PowerShell module capable of working with Network Security.
1. Use a single command line to load the module into memory on both **LON-CL1** and **LON-DC1**.
1. Find a command that can display Windows Firewall rules.
1. Use a single command line to list all enabled firewall rules on both **LON-CL1** and **LON-DC1**.
1. Display only the rule names and the computer name each rule came from.
1. Use a single command line to unload the network security module from memory on both **LON-CL1** and **LON-DC1**.

### Task 3: Create and display an HTML report that displays local disk information from two computers

1. As a test, use **Get-WmiObject** to display a list of local hard drives (the **Win32_LogicalDisk** class, filtered to include only those drives with a drive type of **3**).
1. Use remoting to run the **Get-WmiObject** command against both **LON-DC1** and **LON-CL1**. Don't add a **–ComputerName** parameter to the **Get-WmiObject** command.

   > **Note:** Your report must include each computer’s name, each drive’s letter, and its free space and total size in bytes.

### Task 4: Close all open PSSessions

- In the **Windows PowerShell** console, close all open PSSessions.
