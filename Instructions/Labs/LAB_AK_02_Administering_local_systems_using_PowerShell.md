---
lab:
    title: 'Lab: Performing local system administration with PowerShell'
    type: 'Answer Key'
    module: 'Module 2: Windows PowerShell for local systems administration'
---

# Lab answer key: Performing local system administration with PowerShell

## Exercise 1: Creating and managing Active Directory objects

### Task 1: Create a new organizational unit (OU) for a branch office

1. On **LON-CL1**, select **Start**.

1. Enter **powershell** to display the Windows PowerShell icon. Make sure that the icon name displays **Windows PowerShell** and not **Windows PowerShell (x86)**.

1. Right-click **Windows PowerShell** or activate its context menu, and then select **Run as administrator**.

1. In the **Administrator: Windows PowerShell** window, enter the following command, and then press the Enter key:

   ```powershell
   
   New-ADOrganizationalUnit -Name London
   ```

### Task 2: Create a group for branch office administrators

- In the Windows PowerShell console, enter the following command, and then press the Enter key:

   ```powershell
   New-ADGroup "London Admins" -GroupScope Global
   ```

### Task 3: Create a user and computer account for the branch office

1. In the console, enter the following command, and then press the Enter key:

   ```powershell
   New-ADUser -Name Ty -DisplayName "Ty Carlson" 
   ```

1. Enter the following command, and then press the Enter key:

   ```powershell
   Add-ADGroupMember "London Admins" -Members Ty
   ```

1. Enter the following command, and then press the Enter key:

   ```powershell
   New-ADComputer LON-CL2
   ```

### Task 4: Move the group, user, and computer accounts to the branch office OU

1. In the console, enter the following command, and then press the Enter key:

   ```powershell
   Move-ADObject -Identity "CN=London Admins,CN=Users,DC=Adatum,DC=com" -TargetPath "OU=London,DC=Adatum,DC=com"
   ```

2. Enter the following command, and then press the Enter key:

   ```powershell
   Move-ADObject -Identity "CN=Ty,CN=Users,DC=Adatum,DC=com" -TargetPath "OU=London,DC=Adatum,DC=com"
   ```

3. Enter the following command, and then press the Enter key:

   ```powershell
   Move-ADObject -Identity "CN=LON-CL2,CN=Computers,DC=Adatum,DC=com" -TargetPath "OU=London,DC=Adatum,DC=com"
   ```

### Exercise 1 results

After completing this exercise, you'll have successfully identified and used commands for managing Active Directory objects in the Windows PowerShell command-line interface.

## Exercise 2: Configuring network settings on Windows Server

### Task 1: Test the network connection and review the configuration

1. Switch to **LON-SVR1**.
1. Right-click the **Start** button or activate its context menu, and then select **Windows PowerShell (Admin)**.
1. In the **Administrator: Windows PowerShell** window, enter the following command, and then press the Enter key:

   ```powershell
   Test-Connection LON-DC1
   ```

> **Note:** The test results should be returned without any noticeable delay. You will compare this response time the one after you make changes to the network configuration in this exercise.

1. In the console, enter the following command, and then press the Enter key:

   ```powershell
   Get-NetIPConfiguration
   ```

> **Note:** Note the IP address, default gateway and Domain Name System (DNS) server for **LON-SVR1**.

### Task 2: Change the server IP address

1. In the **Administrator: Windows PowerShell** window, enter the following command, and then press the Enter key:

   ```powershell
   New-NetIPAddress -InterfaceAlias Ethernet -IPAddress 172.16.0.15 -PrefixLength 16
   ```

1. In the console, enter the following command and press the Enter key:

   ```powershell
   Remove-NetIPAddress -InterfaceAlias Ethernet -IPAddress 172.16.0.11
   ```

1. Enter **Y** and press the Enter key for both confirmation prompts.

### Task 3: Change the DNS settings and default gateway for the server

1. In the **Administrator: Windows PowerShell** window, enter the following command, and then press the Enter key:

   ```powershell
   Set-DnsClientServerAddress -InterfaceAlias Ethernet -ServerAddress 172.16.0.12
   ```

2. In the console, enter the following command, and then press the Enter key:

   ```powershell
   Remove-NetRoute -InterfaceAlias Ethernet -DestinationPrefix 0.0.0.0/0 -Confirm:$false
   ```

3. In the console window, enter the following command, and then press the Enter key.

   ```powershell
   New-NetRoute -InterfaceAlias Ethernet -DestinationPrefix 0.0.0.0/0 -NextHop 172.16.0.2
   ```

### Task 4: Verify and test the changes

1. On **LON-SVR1**, in the **Administrator: Windows PowerShell** window, enter the following command, and then press the Enter key:

   ```powershell
   Get-NetIPConfiguration
   ```

> **Note:** Note the IP address, default gateway, and DNS server.

1. In the console, enter the following command, and then press the Enter key:

   ```powershell
   Test-Connection LON-DC1
   ```

> **Note:** Following the change, it should take longer to receive a response from **LON-DC1**. The actual delay might vary. While the change should be large enough to be noticeable, it's possible you won't notice much difference.

### Exercise 2 results

After completing this exercise, you'll have successfully identified and used Windows PowerShell commands for managing network configuration.

## Exercise 3: Creating a website

### Task 1: Install the Web Server (IIS) role on the server

1. On **LON-SVR1**, in the **Administrator: Windows PowerShell** window, enter the following command, and then press the Enter key:

   ```powershell
   Install-WindowsFeature Web-Server
   ```

> **Note:** Wait for Internet Information Services (IIS) to install. This should take about 2 minutes.

### Task 2: Create a folder on the server for the website files

1. On **LON-SVR1**, in the **Administrator: Windows PowerShell** window, enter the following command, and then press the Enter key:

   ```powershell
   New-Item C:\inetpub\wwwroot\London -Type directory
   ```

### Task 3: Create the IIS website

1. On **LON-SVR1**, in the **Administrator: Windows PowerShell** window, enter the following command, and then press the Enter key:

   ```powershell
   New-IISSite London -PhysicalPath C:\inetpub\wwwroot\London -BindingInformation "172.16.0.15:8080:"
   ```

2. On the taskbar, select the **Internet Explorer** icon.

3. In the Address bar, enter `http://172.16.0.15:8080`, and then press the Enter key.

> **Note:** Internet Explorer displays an error message that the web server is configured to not list the contents of this directory. The error message details give the physical path of the site, which should be **C:\\inetpub\\wwwroot\\London**.

### Exercise 3 results

After completing this exercise, you'll have successfully identified and used Windows PowerShell commands that would be used as part of a standardized web server configuration.
