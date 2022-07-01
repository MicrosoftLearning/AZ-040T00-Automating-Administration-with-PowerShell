---
lab:
    title: 'Lab answer key: Configuring Windows PowerShell, and finding and running commands'
    type: 'Answer Key'
    module: 'Module 1: Getting Started with Windows PowerShell'
---

# Lab answer key: Configuring Windows PowerShell, and finding and running commands

## Exercise 1: Configuring the Windows PowerShell console application

### Task 1: Start the console application as Administrator, and pin the Windows PowerShell icon to the taskbar

1. On **LON-CL1**, select **Start**.
1. Enter **powershell** to display the Windows PowerShell icon. Make sure that the icon name displays **Windows PowerShell** and not **Windows PowerShell (x86)**.
1. Right-click **Windows PowerShell** or activate its context menu, and then select **Run as administrator**.
1. Make sure that the window title bar reads **Administrator** and doesn't include the text **(x86)**. This indicates that it is the 64-bit console application and that an administrator is running it.
1. On the taskbar, right-click the **Windows PowerShell** icon or activate its context menu, and then select **Pin to taskbar**. The **Windows PowerShell console** should now be open, run by **Administrator**, and available on the taskbar for future use.

### Task 2: Configure the Windows PowerShell console application

1. To configure Windows PowerShell to use the **Consolas** font:

   a.   Select the control box in the upper-left corner of the **Windows PowerShell console** window.

   b.   Select **Properties**.

   c.    In the **“Windows PowerShell” Properties** dialog box, select the **Font** tab, and then, in the **Font** list, select **Consolas**.

   d.   Select **16** in the **Size** list.

1. To select alternate display colors, on the **Colors** tab, review the available **Screen Text** and **Screen Background** colors.

    > **Note:** Experiment with various combinations. You can use the color picker to change colors quickly to improve readability.

1. To resize the window and remove the horizontal scroll bar:

   a.   On the **Layout** tab, in the **Window Size** settings, change the area’s **Width** and **Height** values until the **Windows PowerShell** console pane preview fits completely within the **Window Preview** area.

   b.   On the **Layout** tab, in the **Screen Buffer** **Size** settings, change the **Width** value to be the same as the **Width** value in the **Windows Size** settings.

1. Select **OK**. The console application should be ready for use.

### Task 3: Start a shell transcript

- In the **Windows PowerShell console**, enter the following command, and then press the Enter key:

   ```ps
   Start-Transcript C:\DayOne.txt
   ```

    > **Note:** You've now started a transcript of your Windows PowerShell session. It'll save all the commands you enter and the command output to the text file until you run **Stop‑Transcript** or close the Windows PowerShell window. You can review the contents of the transcript at any time by opening **C:\DayOne.txt**.

### Exercise 1 results

After completing this exercise, you'll have opened and configured the Windows PowerShell console application and configured its appearance and layout.

## Exercise 2: Configuring the Windows PowerShell ISE application

### Task 1: Open the Windows PowerShell ISE application as Administrator

1. In the **Windows PowerShell console**, enter **ise**, and then press the Enter key.

   > **Note:** This method of opening the ISE will work correctly only when an administrator is running the console.

1. Close the ISE window.

1. Right-click the **Windows PowerShell** icon on the taskbar or activate its context menu, and then select **Run ISE as Administrator**. You should now be running Windows PowerShell ISE as **Administrator**.

### Task 2: Customize the ISE's appearance to use a single-pane view, hide the Command pane, and adjust the font size

1. To configure the ISE to use the single-pane view:

    a. On the **Windows PowerShell ISE** toolbar, select the **Show Script Pane Maximized** option.
    
    b. Select the **Hide Script Pane** up-arrow icon to display the console.
    
    > **Note:** Alternatively, you can press the **Ctrl+R** key combination.

1. Select the **Show** **Command Add-on** option to review the **Commands** pane, if it isn't showing.

1. Select the **Show Command Add-on** option to hide the **Commands** pane.

1. Use the slider in the lower-right corner of the window to adjust the font size until you can review it comfortably.

1. Close the **Windows PowerShell ISE** and the **Windows PowerShell** windows.

### Exercise 2 results

After completing this exercise, you'll have customized the appearance of the Windows PowerShell Integrated Scripting Environment (ISE) application.

## Exercise 3: Finding and running Windows PowerShell commands

### Task 1: Find commands that'll accomplish specified tasks

1. On **LON-CL1**, on the task bar, right‑click **Windows PowerShell**, and then select **Run as Administrator**.

1. In the console, enter one of the following commands, and then press the Enter key:

   ```ps
   Get-Help *resolve* 
   ```

   or:

   ```ps
   Get-Command *resolve* 
   ```

   or:

   ```ps
   Get-Command -Verb resolve 
   ```

   > **Note:** The first two commands display a list of commands that use *Resolve* anywhere in their names. The third displays a list of commands that use the verb *Resolve* in their name. All three will return the same results in the lab environment. This should lead you to the **Resolve-DNSName** command.

1. In the console, enter one of the following commands, and then press the Enter key:

   ```ps
   Get-Help *adapter* 
   ```

   or:

   ```ps
   Get-Command *adapter* 
   ```

   or:

   ```ps
   Get-Command -Noun *adapter*
   ```

   or:

   ```ps
   Get-Command -Verb Set -Noun *adapter* 
   ```

   > **Note:** The first three commands display a list of commands that use *Adapter* in their names. The fourth displays a list of commands that have *Adapter* in their names and use the *Set* verb. This should lead you to the **Set-NetAdapter** command.

1. Run **Get-Help Set-NetAdapter** to review the help for that command. This should lead you to the *‑MACAddress* parameter.

1. In the console, enter one of the following commands, and then press the Enter key:

   ```ps
   Get-Help *sched* 
   ```

   or:

   ```ps
   Get-Command *sched* 
   ```

   or:

   ```ps
   Get-Module *sched* -ListAvailable
   ```

   > **Note:** The first two commands display a list of commands that use *Sched* in their name. The third displays a list of modules with *Sched* in their name, which should lead you to the module **ScheduledTasks**. If you then run the command `Get-Command -Module *ScheduledTasks*`, you'll get a list of commands in that module. This should lead you to the **Enable-ScheduledTask** command.

1. In the console, enter one of the following commands, and then press the Enter key:

   ```ps
   Get-Command –Verb Block 
   ```

   or:

   ```ps
   Get-Help *block* 
   ```

   > **Note:** These display a list of commands, which should lead you to the **Block-SmbShareAccess** command. Then, run **Get-Help Block-SmbShareAccess** to learn that the command applies a Deny entry to the file share discretionary access control list (DACL).

1. In the console, enter the following command, and then press the Enter key:

   ```ps
   Get-Help *branch*
   ```

   > **Note:** This will cause the help system to conduct a full-text search, because no commands use *branch* in their names.

   A list of topics containing the text *branch* displays, but none appear related to clearing the **BranchCache** cache.

1. In the console, enter one of the following commands, and then press the Enter key:

   ```ps
   Get-Help *cache* 
   ```

   or:

   ```ps
   Get-Command *cache* 
   ```

   or:

   ```ps
   Get-Command -Verb clear
   ```

   > **Note:** The first two commands will display a list of commands containing *Cache* in the name. The third displays a list of commands using the verb *Clear* in the name. Either way, you should discover the **Clear-BCCache** command.

1. In the console, enter one of the following commands, and then press the Enter key:

   ```ps
   Get-Help *firewall*
   ```

   or:

   ```ps
   Get-Command *firewall* 
   ```

   or:

   ```ps
   Get-Help *rule*
   ```

   or:

   ```ps
   Get-Command *rule* 
   ```

   > **Note:** These display a list of commands that use those words in their names, which should lead you to the **Get-NetFirewallRule** command.

1. In the console, enter the following command, and then press the Enter key:

   ```ps
   Get-Help Get-NetFirewallRule –Full
   ```

   > **Note:** This will display the help for the command, so you can discover the *–Enabled* parameter.

1. In the console, enter the following command, and then press the Enter key:

   ```ps
   Get-Help *address* 
   ```

   > **Note:** This will display a list of commands that use *address* in their names. This should lead you to the **Get-NetIPAddress** command.

1. In the console, enter the following command, and then press the Enter key:

   ```ps
   Get-Command –Verb suspend
   ```

   > **Note:** This displays a list of commands that use the verb *Suspend* in their names. This should lead you to the **Suspend-PrintJob** command.

1. In the console, enter one of the following commands, and then press the Enter key:

   ```ps
   Get-Alias Type
   ```

   or:

   ```ps
   Get-Command –Noun *content* 
   ```

   > **Note:** The first command displays the alias definition for the **Type** command, which is the command used in **cmd.exe** to review text from a file. The second command returns a list of commands with *Content* in the noun portion of the name. This should lead you to the **Get-Content** command.

### Task 2: Run commands to accomplish specified tasks

1. Ensure you are signed in on the **LON-CL1** virtual machine as **Adatum\\Administrator**.

2. To display a list of enabled firewall rules, in the console, enter the following command, and then press the Enter key:

   ```ps
   Get-NetFirewallRule -Enabled True
   ```

3. To display a list of all local IPv4 addresses, in the console, enter the following command, and then press the Enter key:

   ```ps
   Get-NetIPAddress –AddressFamily IPv4
   ```

4. To set the startup type of the Background Intelligent Transfer Service (BITS), in the console, enter the following command, and then press the Enter key:

   ```ps
   Set-Service –Name BITS –StartupType Automatic 
   ```

5. To test the connection to **LON-DC1**, in the console, enter the following command, and then press the Enter key:

   ```ps
   Test-Connection –ComputerName LON-DC1 –Quiet
   ```

   > **Note:** This command returns only a True or False value, without any other output.

6. To display the newest 10 entries from the Security event log, in the console, enter the following command, and then press the Enter key:

   ```ps
   Get-EventLog –LogName Security –Newest 10 
   ```

### Exercise 3 results

After completing this exercise, you'll have demonstrated your ability to find and run Windows PowerShell commands that perform specific tasks.

## Exercise 4: Using About files

### Task 1: Locate and review About help files

1. Ensure you're still signed in to **LON-CL1** as **Adatum\\Administrator** from the previous exercise.

1. To find operators used for wildcard string comparison, in the console, enter the following command, and then press the Enter key:

   ```ps
   Get-Help *comparison*
   ```

1. In the console, enter the following command, and then press the Enter key:

   ```ps
   Get-Help about_comparison_operators -ShowWindow
   ```

   Notice the **–Like** operator in the **about_Comparison_Operators Help**, which displays in a modal window.

1. To find the **-Like** operator, in the **Find** text box, enter **wildcard**, and then select **Next**.

1. After reviewing the **about_Comparison_Operators** file, you should learn that typical operators are not case-sensitive. Specific case-sensitive operators are provided in **about_Comparison_Operators**.

1. To display the **COMPUTERNAME** environment variable, in the console, enter the following command, and then press the Enter key:

   ```ps
   $env:computername
   ```

   You could learn about this technique in **about_environment_variables**.

1. In the console, enter the following command, and then press the Enter key:

   ```ps
   Get-Help *signing*
   ```

1. In the console, enter the following command, and then press the Enter key:

   ```ps
   Get-Help about_signing 
   ```

1. Learn about code signing. You should learn that **MakeCert.exe** is used to create a self-signed digital certificate.

### Exercise 4 results

After completing this exercise, you'll have demonstrated your ability to locate help content in **About** files.
