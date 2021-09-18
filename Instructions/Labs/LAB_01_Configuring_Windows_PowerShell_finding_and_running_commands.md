---
lab:
    title: 'Lab: Configuring Windows PowerShell, and finding and running commands' 
    module: 'Module 1: Getting Started with Windows PowerShell'
--- 

# Lab: Configuring Windows PowerShell, and finding and running commands

## Scenario

You're an administrator who'll use Windows PowerShell to automate many administrative tasks. You must ensure that you can successfully start the correct Windows PowerShell host applications and configure them for future use by customizing their appearance.

You're also preparing to complete several administrative tasks by using Windows PowerShell. You need to discover commands that you'll use to perform those tasks, run several commands to begin performing those tasks, and learn about new Windows PowerShell features that'll enable you to complete those tasks.

## Objectives

After completing this lab, you'll be able to:

- Open and configure the Windows PowerShell console application.
- Open and configure the Windows PowerShell ISE application.
- Find and run Windows PowerShell commands.
- Use Windows PowerShell Help and About topics to learn new shell concepts and techniques.

## Estimated time: 60 minutes

## Lab Setup

Virtual machines: **AZ-040T00A-LON-DC1** and **AZ-040T00A-LON-CL1**

User name: **Adatum\\Administrator**

Password: **Pa55w.rd**

## Lab Startup

1. Select  **LON-DC1**.
1. Sign in by using the following credentials:
   - User name: **Administrator**
   - Password: **Pa55w.rd**
   - Domain: **Adatum**

1. Repeat these steps for **LON-CL1**.

## Exercise 1: Configuring the Windows PowerShell console application

### Exercise scenario 1

To customize Windows PowerShell, you need to first make changes to the console. In this exercise, you'll open the Windows PowerShell console application and configure its appearance and layout.

The main tasks for this exercise are:

1. Start the console application as Administrator, and pin the Windows PowerShell icon to the taskbar.
1. Configure the Windows PowerShell console application.
1. Start a shell transcript.

### Task 1: Start the console application as Administrator, and pin the Windows PowerShell icon to the taskbar

1. On **LON-CL1**, start the **Windows PowerShell** application as **Administrator**. Make sure that the window title bar reads **Administrator** and doesn't include the text (x86). This indicates that it's the 64-bit console application and that an administrator is running it.
1. Pin the Windows PowerShell icon to the taskbar.

### Task 2: Configure the Windows PowerShell console application

1. Open **Windows PowerShell Properties**, and then configure Windows PowerShell to use the **Consolas** font with **16**-point size.
2. From the **Colors** tab, select alternate display colors for the primary text and background.
3. From the **Layout** tab, size the window to fit on the screen and remove any horizontal scroll bar.

### Task 3: Start a shell transcript

1. In the Windows PowerShell console, enter the following command, and then select Enter:

   ```ps
   Start-Transcript C:\DayOne.txt
   ```

> **Note:** You've now started a transcript of your Windows PowerShell session. It'll save all commands that you enter and the command output to a text file until you run **Stop‑Transcript** or close the Windows PowerShell window. You can review the transcript's contents at any time by opening **C:\DayOne.txt**.

### Exercise 1 results

After completing this exercise, you'll have opened and configured the Windows PowerShell console application and its appearance and layout.

## Exercise 2: Configuring the Windows PowerShell ISE application

### Exercise Scenario 2

In this exercise, you'll customize the appearance of the Windows PowerShell ISE application.

The main tasks for this exercise are:

1. Open the Windows PowerShell ISE application as Administrator.
1. Customize the appearance of the ISE to use the single-pane view, hide the **Command** pane, and adjust the font size.

### Task 1: Open the Windows PowerShell ISE application as Administrator

1. Right-click the **Windows PowerShell** icon on the taskbar or activate its context menu, and then open the **Windows PowerShell ISE** application as **Administrator**.

### Task 2: Customize the ISE's appearance to use a single-pane view, hide the Command pane, and adjust the font size

1. Configure the ISE to use the single-pane view and display the console pane.
2. Hide the **Command** pane.
3. Adjust the font size so that you can review it comfortably.
4. Close the **Windows PowerShell ISE** and the **Windows PowerShell** windows.

### Exercise 2 results

After completing this exercise, you'll have customized the appearance of the Windows PowerShell ISE application.

## Exercise 3: Finding and running Windows PowerShell commands

### Exercise Scenario 3

In this exercise, you'll use Windows PowerShell’s **Get-Help** and **Get-Command** commands to discover new commands that can complete specific tasks within Windows PowerShell. You'll also run several basic Windows PowerShell commands. In some instances, you might have to find the commands that you'll use to complete the task.

The main tasks for this exercise are:

1. Find commands that'll accomplish specified tasks.
1. Run commands to accomplish specified tasks.

### Task 1: Find commands that'll accomplish specified tasks

- On **LON-CL1**, ensure that you're signed in as **Adatum\\Administrator** and determine the answers to the following questions:

  - What command would you run to resolve a DNS name?
  - What command would you run to make changes to a network adapter? After finding such a command, what parameter would you use to change its Media Access Control (MAC) address (on adapters that support changes to their MAC address)?
  - What command would let you enable a previously disabled scheduled task?
  - What command would let you block access to a file share by a particular user?
  - What command would you run to clear your computer’s local **BranchCache** cache?
  - What command would you run to display a list of Windows Firewall rules? What parameter of that command would display only enabled rules?
  - What command would you run to display a list of all locally bound IP addresses?
  - What command would you run to suspend an active print job in a print queue?
  - What native Windows PowerShell command would you run to review the content of a text file?

### Task 2: Run commands to accomplish specified tasks

1. Ensure you are signed in on the **LON-CL1** virtual machine as **Adatum\\Administrator**.

2. Display a list of enabled Windows Firewall rules.

3. Display a list of all local IPv4 addresses.

4. Set the startup type of the BITS service to **Automatic**:

   a.   Open the **Computer Management** console, and then go to **Services and Applications**.

   b.   Locate the Background Intelligence Transfer Service (BITS) and note its startup type setting prior to and after changing the startup type in Windows PowerShell.

5. Test the network connection to **LON-DC1**. Your command should return only a True or False value, without any other output.

6. Display the newest 10 entries from the local Security event log.

### Exercise 3 results

After completing this exercise, you'll have demonstrated your ability to find and run Windows PowerShell commands that perform specific tasks.

## Exercise 4: Using About files

### Exercise Scenario 4

In this exercise, you'll use help discovery techniques to find content in **About** files, and then use that content to answer questions about global Windows PowerShell functionality.

Remember that you must use **Get-Help** and wildcard characters. **About** files aren't commands, **Get-Command** will not be useful in this exercise.

The main task for this exercise is:

- Locate and review **About** help files.

### Task 1: Locate and review About help files

- Ensure that you'll still signed in to **LON-CL1** as **Adatum\\Administrator** from the previous exercise, and answer the following questions:

  - What comparison operator does Windows PowerShell use for wildcard string comparisons?
  - Are Windows PowerShell comparison operators typically case-sensitive?
  - How would you use `$Env` to display the **COMPUTERNAME** environment variable?
  - What external command could you use to create a self-signed digital certificate that's usable for signing Windows PowerShell scripts?

### Exercise 4 results

After completing this exercise, you'll have demonstrated your ability to locate help content in **About** files.
