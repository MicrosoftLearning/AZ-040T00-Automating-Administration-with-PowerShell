---
lab:
  title: 'Lab: Using scripts with PowerShell'
  type: Answer Key
  module: 'Module 7: Windows PowerShell scripting'
  description: Build and run PowerShell scripts that include looping, conditional logic, and CSV driven account creation. You apply code signing and execution policy concepts, then add alternate credential support for remote disk queries.
  duration: 150 minutes
  level: 300
  islab: true
  primarytopics:
    - PowerShell Scripting
    - Code Signing
    - CSV
    - Credential Management
---

# Using scripts with PowerShell

This lab should take approximately **150** minutes to complete.

## Scenario

You've started to develop Windows PowerShell scripts to simplify administration in your organization. There are multiple tasks to accomplish, and you'll create a Windows PowerShell script for each one.

## Objectives

After completing this lab, you'll be able to:

- Digitally sign a script.
- Process an array by using ForEach.
- Process items by using If statements.
- Create user accounts based on a CSV file.
- Query disk information from remote computers.
- Update a script to use alternate credentials.

## Lab setup

Virtual machines: **LON-DC1**, **LON-SVR1**, and **LON-CL1**

User name: **Adatum\\Administrator**

Password: **Pa55w.rd**

For this lab, you'll use the available virtual machine environment. Before you begin the lab, complete the following steps:

1. Open **LON-DC1** and sign in as **Adatum\\Administrator** with the password **Pa55w.rd**.
1. Repeat step 1 for **LON-SVR1** and **LON-CL1**.

## Exercise 1: Signing a script

### Exercise scenario 1

To enhance security, you're considering a requirement that all Windows PowerShell scripts in your environment be digitally signed. Before implementing this requirement, you want to test the process.

The main tasks for this exercise are:

1. Install a code signing certificate.
1. Digitally sign a script.
1. Set the execution policy.

### Task 1: Install a code signing certificate

1. On **LON-CL1**, select **Start**, enter **mmc.exe**, and then select **mmc.exe**.
1. In the **MMC** console, select **File**, and then select **Add/Remove Snap-in**.
1. In the **Add or Remove Snap-ins** window, select **Certificates**, and then select **Add**.
1. In the **Certificates snap-in** dialog box, select **My user account**, and then select **Finish**.
1. In the **Add or Remove Snap-ins** window, select **OK**.
1. In the **MMC** console, expand **Certificates - Current User**, and then select **Personal**.
1. Right-click **Personal** or activate its context menu, hover over **All Tasks**, and then select **Request New Certificate**.
1. In the **Certificate Enrollment** wizard, on the **Before You Begin** page, select **Next**.
1. On the **Select Certificate Enrollment Policy** page, select **Active Directory Enrollment Policy**, and then select **Next**.
1. On the **Request Certificates** page, select the **Adatum Code Signing** checkbox, and then select **Enroll**.
1. On the **Certificate Installation Results** page, select **Finish**.
1. In the **MMC** console, expand **Personal**, and then select **Certificates** to verify that the new code signing certificate is present.
1. Close the **MMC** console and select **No** at the prompt to save the console settings.

### Task 2: Digitally sign a script

1. Select the **Start** button, enter **Powersh**, and then select **Windows PowerShell**.
1. At the Windows PowerShell prompt, enter the following command, and then press the Enter key:

   ```powershell
   Get-ChildItem Cert:\CurrentUser\My\ -CodeSigningCert
   ```

1. At the Windows PowerShell prompt, enter the following command, and then press the Enter key:

   ```powershell
   $cert = Get-ChildItem Cert:\CurrentUser\My\ -CodeSigningCert
   ```

1. At the Windows PowerShell prompt, enter the following command, and then press the Enter key:

   ```powershell
   Set-Location E:\Mod07\Labfiles
   ```

1. At the Windows PowerShell prompt, enter the following command, and then press the Enter key:

   ```powershell
   Rename-Item HelloWorld.txt HelloWorld.ps1
   ```

1. At the Windows PowerShell prompt, enter the following command, and then press the Enter key:

   ```powershell
   Set-AuthenticodeSignature -FilePath HelloWorld.ps1 -Certificate $cert
   ```

### Task 3: Set the execution policy

1. At the Windows PowerShell prompt, enter the following command, and then press the Enter key. Enter **Y** at the prompt and press the Enter key:

   ```powershell
   Set-ExecutionPolicy AllSigned
   ```

2. At the Windows PowerShell prompt, enter the following command, and then press the Enter key. You might be asked if you want to run software from the untrusted publisher. Enter **A** and then press the Enter key:

   ```powershell
   .\HelloWorld.ps1
   ```

3. At the Windows PowerShell prompt, enter the following command, and then press the Enter key. Enter **Y** at the prompt and press the Enter key:

   ```powershell
   Set-ExecutionPolicy Unrestricted
   ```

4. Close the Windows PowerShell prompt.

## Exercise 2: Processing an array with a ForEach loop

### Scenario 2

Adatum Corporation is testing a new Voice over IP (VoIP) and video-conferencing system. To support this system, you must set the **ipPhone** attribute for a group of test users. The naming convention that's been selected for the **ipPhone** attribute is **FirstName.LastName@adatum.com**.

The main tasks for this exercise are:

1. Create a test group.
1. Create a script to configure the `ipPhone` attribute.

### Task 1: Create a test group

1. On **LON-CL1**, select **Start**, enter **Powersh**, and then select **Windows PowerShell**.

1. At the Windows PowerShell prompt, enter the following command, and then press the Enter key:

   ```powershell
   New-ADGroup -Name IPPhoneTest -GroupScope Universal -GroupCategory Security
   ```

1. At the Windows PowerShell prompt, enter the following command, and then press the Enter key:

   ```powershell
   Move-ADObject "CN=IPPhoneTest,CN=Users,DC=Adatum,DC=com" -TargetPath "OU=IT,DC=Adatum,DC=com"
   ```

1. At the Windows PowerShell prompt, enter the following command, and then press the Enter key:

   ```powershell
   Add-ADGroupMember IPPhoneTest -Members Abbi,Ida,Parsa,Tonia
   ```

### Task 2: Create a script to configure the ipPhone attribute

- A script that performs this task is located at **E:\\Mod07\\Labfiles\\AZ-040_Mod07_Ex2_LAK.txt**.

## Exercise 3: Processing items by using If statements

Some of the servers in your organization have services that don't start properly when the server is restarted. You want to create a script that can be used to start a specified list of services. When you've performed sufficient testing, you plan to configure a scheduled task that runs the script. During the testing phase, you'll work with the Windows Time and Print Spooler services.

The main tasks for this exercise are:

1. Create services.txt with service names.
1. Create a script that starts stopped services.

### Task 1: Create services.txt with service names

1. Select **Start**, enter **powersh**, and then select **Windows PowerShell**.
1. At the Windows PowerShell prompt, enter the following command, and then press the Enter key:

   ```powershell
   Set-Location E:\Mod07\Labfiles
   ```

1. At the Windows PowerShell prompt, enter the following command, and then press the Enter key:

   ```powershell
   New-Item services.txt -ItemType File
   ```

1. At the Windows PowerShell prompt, enter the following command, and then press the Enter key:

   ```powershell
   Get-Service "Print Spooler" | Select -ExpandProperty Name | Out-File services.txt -Append
   ```

1. At the Windows PowerShell prompt, enter the following command, and then press the Enter key:

   ```powershell
   Get-Service "Windows Time" | Select -ExpandProperty Name | Out-File services.txt -Append
   ```

### Task 2: Create a script that starts stopped services

- A script that performs this task is located at **E:\\Mod07\\Labfiles\\AZ-040_Mod07_Ex3_LAK.txt**.

## Exercise 4: Creating users based on a CSV file

### Exercise scenario 4

The helpdesk for Adatum creates user accounts once per week based on data provided by the Human Resources department. This data is provided in a CSV file.

There have been multiple instances where the new user accounts weren't created with the correct information. The helpdesk has been using the CSV files as a reference and creating the user accounts by using graphical tools. You want to automate this process to avoid these errors.

The main task for this exercise is:

- Create AD DS users from a CSV file.

### Task 1: Create AD DS users from a CSV file

- A script that performs this task is located at **E:\\Mod07\\Labfiles\\AZ-040_Mod07_Ex4_LAK.txt**.

## Exercise 5: Querying disk information from remote computers

### Exercise scenario 5

Adatum hasn't documented the logical disk configuration for all of the computers. As part of gathering the information for your documentation, you're creating a script to gather logical disk information.

Your script for disk information has the following requirements:

- Accept the remote computer name as a parameter.
- If no computer name is provided as a parameter, the user should be prompted to enter a computer name.
- The query for information should use Web Services-Management (WS-MAN) rather than Distributed Component Object Model (DCOM).
- Display logical disk information (volumes) rather than physical disk information.
- Only information for local disks (hard drives) should be included.

The main task for this exercise is:

- Create a script that queries disk information with current credentials.

### Task 1: Create a script that queries disk information with current credentials

1. Perform all steps using **LON-CL1**.
1. A script that performs this task is located at **E:\\Mod07\\Labfiles\\AZ-040_Mod07_Ex5_LAK.txt**.

## Exercise 6: Updating the script to use alternate credentials

### Exercise scenario 6

You'd like to run a script that queries disk information from remote computers. To account for scenarios where the user doesn't have permission to query disk information on remote servers, you're updating the script to accept alternate credentials when specified.

The script needs to meet the following requirements:

- Accept a switch parameter to indicate whether alternate credentials are required.
- If alternate credentials are required, gather and use those credentials.

The main task for this exercise is:

- Update the script to use alternate credentials.

### Task 1: Update the script to use alternate credentials

- A script that performs this task is located at **E:\\Mod07\\Labfiles\\AZ-040_Mod07_Ex6_LAK.txt**.
