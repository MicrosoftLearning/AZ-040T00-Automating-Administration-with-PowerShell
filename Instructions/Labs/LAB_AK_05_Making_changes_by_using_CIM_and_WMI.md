---
lab:
    title: 'Lab: Querying information by using WMI and CIM'
    type: 'Answer Key'
    module: 'Module 5: Querying management information by using CIM and WMI'
---

# Lab answer key: Querying information by using WMI and CIM

## Exercise 1: Querying information by using WMI

### Task 1: Query IP addresses

1. On **LON-CL1**, select **Start**, and then enter **powersh**.
1. In the results list, right-click **Windows PowerShell** or activate its context menu, and then select **Run as administrator**.
1. To find a repository class that lists the IP addresses being used by a computer, enter the following command in the **Windows PowerShell** console, and then press the Enter key:

   ```powershell
   Get-WmiObject -Namespace root\cimv2 -List | Where Name -like '*configuration*' | Sort Name
   ```

   Notice the `Win32_NetworkAdapterConfiguration` class.

1. To retrieve all instances of the class depicting static IP addresses, enter the following command in the **Windows PowerShell** console, and then press the Enter key:

   ```powershell
   Get-WmiObject -Class Win32_NetworkAdapterConfiguration | Where DHCPEnabled -eq $False | Select IPAddress
   ```

   Remember that you can run the first command and pipe its output to **Get-Member** to review the properties that are available.

### Task 2: Query operating system version information

1. To find a repository class that lists operating system information, enter the following command in the **Windows PowerShell** console, and then press the Enter key:

   ```powershell
   Get-WmiObject -Namespace root\cimv2 -List | Where Name -like '*operating*' | Sort Name
   ```

   Notice the `Win32_OperatingSystem` class.

1. To display a list of properties for the class, enter the following command in the **Windows PowerShell** console, and then press the Enter key:

   ```powershell
   Get-WmiObject -Class Win32_OperatingSystem | Get-Member
   ```

1. Notice the **Version**, **ServicePackMajorVersion**, and **BuildNumber** properties.

1. To display the specified information, enter the following command in the **Windows PowerShell** console, and then press the Enter key:

   ```powershell
   Get-WmiObject -Class Win32_OperatingSystem | Select Version,ServicePackMajorVersion,BuildNumber
   ```

   

### Task 3: Query computer system hardware information

1. To find a repository class that displays computer system information, enter the following command in the **Windows PowerShell** console, and then press the Enter key:

    ```powershell
    Get-WmiObject -Namespace root\cimv2 -List | Where Name -like '*system*' | Sort Name 
    ```

    Notice the `Win32_ComputerSystem` class.

1. To display a list of instance properties and values, enter the following command in the **Windows PowerShell** console, and then press the Enter key:

   ```powershell
   Get-WmiObject -Class Win32_ComputerSystem | Format-List -Property *
   ```

   Remember that `Get-Member` doesn't display property values, but `Format-List` can.

1. To display the specified information, enter the following command in the **Windows PowerShell** console, and then press the Enter key:

   ```powershell
   Get-WmiObject -Class Win32_ComputerSystem | Select Manufacturer,Model,@{n='RAM';e={$PSItem.TotalPhysicalMemory}}
   ```


### Task 4: Query service information

1. To find a repository class that contains information about services, enter the following command in the **Windows PowerShell** console, and then press the Enter key:
    
    ```powershell
    Get-WmiObject -Namespace root\cimv2 -List | Where Name –like '*service*' | Sort Name
    ```
    
    Notice the `Win32_Service` class.
    
1. To display a list of instance properties and values, enter the following command in the **Windows PowerShell** console, and then press the Enter key:
   
   ```powershell
   Get-WmiObject -Class Win32_Service | FL *
   ```
   
1. To display the specified information, enter the following command in the **Windows PowerShell** console, and press the Enter key:
   
   ```powershell
   Get-WmiObject –Class Win32_Service –Filter "Name LIKE 'S%'" | Select Name,State,StartName
   ```
   
1. Leave the **Windows PowerShell** console open for the next exercise.

## Exercise 2: Querying information by using CIM

### Task 1: Query user accounts

1. To find a repository class that lists user accounts, enter the following command in the **Windows PowerShell** console, and then press the Enter key:
   
   ```powershell
   Get-CimClass -ClassName *user*
   ```
   
   Notice the `Win32_UserAccount` class.
   
1. To display a list of class properties, enter the following command in the **Windows PowerShell** console, and then press the Enter key:
   
   ```powershell
   Get-CimInstance -Class Win32_UserAccount | Get-Member
   ```
   
1. To display the specified information, enter the following command in the **Windows PowerShell** console, and then press the Enter key:
   
   ```powershell
   Get-CimInstance -Class Win32_UserAccount | Format-Table -Property Caption,Domain,SID,FullName,Name
   ```
   
   Notice the returned list of all domain and local accounts.

### Task 2: Query BIOS information

1. To find a repository class that contains BIOS information, enter the following command in the **Windows PowerShell** console, and then press the Enter key:

    ```powershell
    Get-CimClass -ClassName *bios*
    ```

    Notice the `Win32_BIOS` class.

1. To display the specified information, enter the following command in the **Windows PowerShell** console, and then press the Enter key:

    ```powershell
    Get-CimInstance -Class Win32_BIOS
    ```    

### Task 3: Query network adapter configuration information

1. To display a list of all the local `Win32_NetworkAdapterConfiguration` instances, enter the following command in the **Windows PowerShell** console, and then press the Enter key:
   
   ```powershell
   Get-CimInstance -Classname Win32_NetworkAdapterConfiguration
   ```
   
1. To display a list of all the `Win32_NetworkAdapterConfiguration` instances that exist on **LON-DC1**, enter the following command in the **Windows PowerShell** console, and then press the Enter key:
   
   ```powershell
   Get-CimInstance -Classname Win32_NetworkAdapterConfiguration -ComputerName LON-DC1
   ```

### Task 4: Query user group information

1. To find a repository class that lists user groups, enter the following command in the **Windows PowerShell** console, and then press the Enter key:

    ```powershell
    Get-CimClass -ClassName *group*
    ```

    Notice the `Win32_Group` class.

1. To display the specified information, enter the following command in the **Windows PowerShell** console, and then press the Enter key:

    ```powershell
    Get-CimInstance -ClassName Win32_Group -ComputerName LON-DC1
    ```

1. Leave the **Windows PowerShell** console open for the next exercise.

## Exercise 3: Invoking methods

### Task 1: Invoke a CIM method

1. To restart **LON-DC1**, enter the following command in the **Windows PowerShell** console, and then press the Enter key:
   
    ```powershell
    Invoke-CimMethod -ClassName Win32_OperatingSystem -ComputerName LON-DC1 -MethodName Reboot
    ```
   Notice the response that includes **ReturnValue=0** and **PSComputerName=LON-DC1**.
1. Switch to the **LON-DC1** virtual machine and observe it restarting.
1. When the restart is complete, switch back to the **LON-CL1** virtual machine.

### Task 2: Invoke a WMI method

1. To review properties of the WinRM service, enter the following command in the **Windows PowerShell** console, and then press the Enter key:
    
    ```powershell
    Get-Service WinRM | FL *
    ```
    Note that the **StartType** is **Manual**.
1. To change the start mode of the specified service, enter the following command in the **Windows PowerShell** console, and then press the Enter key:
    
    ```powershell
    Get-WmiObject -Class Win32_Service -Filter "Name='WinRM'" | Invoke-WmiMethod -Name ChangeStartMode -Argument 'Automatic'
    ```
1. To verify that the StartType of the WinRM service has changed, enter the following command in the **Windows PowerShell** console, and then press the Enter key:
   
    ```powershell
    Get-Service WinRM | FL *
    ```

   Note that the **StartType** is **Automatic**.
