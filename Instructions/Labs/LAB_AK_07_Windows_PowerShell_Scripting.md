---
lab:
    title: 'Lab: Using scripts with PowerShell'
    type: 'Answer Key'
    module: 'Module 7: Windows PowerShell scripting'
---

# Lab answer key: Using scripts with PowerShell

## Exercise 1: Signing a script

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

### Task 1: Create AD DS users from a CSV file

- A script that performs this task is located at **E:\\Mod07\\Labfiles\\AZ-040_Mod07_Ex4_LAK.txt**.

## Exercise 5: Querying disk information from remote computers

### Task 1: Create a script that queries disk information with current credentials

1. Perform all steps using **LON-CL1**.
1. A script that performs this task is located at **E:\\Mod07\\Labfiles\\AZ-040_Mod07_Ex5_LAK.txt**.

## Exercise 6: Updating the script to use alternate credentials

### Task 1: Update the script to use alternate credentials

- A script that performs this task is located at **E:\\Mod07\\Labfiles\\AZ-040_Mod07_Ex6_LAK.txt**.
