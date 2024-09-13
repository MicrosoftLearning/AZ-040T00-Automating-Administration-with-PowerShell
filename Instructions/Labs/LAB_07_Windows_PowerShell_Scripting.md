---
lab:
    title: 'Lab: Using scripts with PowerShell'
    module: 'Module 7: Windows PowerShell scripting'
---

# Lab: Using scripts with PowerShell

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

## Estimated time: 150 minutes

## Lab setup

- Virtual machines: **LON-DC1**, **LON-SVR1**, and **LON-CL1**
- User name: **Adatum\\Administrator**
- Password: **Pa55w.rd**

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

1. On **LON-CL1**, open an **MMC** console, and then add the **Certificates** snap-in focused on **My user account**.
1. In the **MMC** console, browse to **Certificates - Current User\\Personal**.
1. Use the context menu of the **Personal** folder and select **Request New Certificate**.
1. Use the following settings in the **Certificate Enrollment** wizard:

   - **Active Directory Enrollment Policy**
   - **Adatum Code Signing** template

1. In the **MMC** console, verify that the new code-signing certificate is present.
1. Close the **MMC** console.

### Task 2: Digitally sign a script

1. Open a Windows PowerShell prompt.
1. Place the code-signing certificate in **Cert:\CurrentUser\My** into a variable.
1. In **E:\Mod07\Labfiles**, rename **HelloWorld.txt** to **HelloWorld.ps1**.
1. Use the **Set-Authenticode** cmdlet to apply a digital signature to **HelloWorld.ps1**.

### Task 3: Set the execution policy

1. On **LON-CL1**, set the execution policy to allow only signed scripts.
1. Verify that you can run **HelloWorld.ps1**.
1. Set the execution policy to **Unrestricted**.

## Exercise 2: Processing an array with a ForEach loop

### Scenario 2

Adatum Corporation is testing a new Voice over IP (VoIP) and video-conferencing system. To support this system, you must set the **ipPhone** attribute for a group of test users. The naming convention that's been selected for the **ipPhone** attribute is **FirstName.LastName@adatum.com**.

The main tasks for this exercise are:

1. Create a test group.
1. Create a script to configure the `ipPhone` attribute.

### Task 1: Create a test group

1. On **LON-CL1**, use PowerShell to create a new Active Directory Domain Services (AD DS) group named **IPPhoneTest** in the **IT** organizational unit.
1. Add the following users as members in the **IPPhoneTest** group:

   - **Abbi Skinner**
   - **Ida Alksne**
   - **Parsa Schoonen**
   - **Tonia Guthrie**

### Task 2: Create a script to configure the ipPhone attribute

1. Create a script named **E:\\Mod07\\Labfiles\\ipPhone.ps1**, and then open it in the Windows PowerShell ISE.
1. Use **Get-ADGroupMember** to create a query to obtain the membership of the **IPPhoneTest** group.
1. Create a **ForEach** loop that processes the users that are members of **IPPhoneTest**.
1. In the loop:

   - Use **Get-ADUser** to retrieve the first and last names for a user.
   - Calculate the required value for the **ipPhone** attribute.
   - Use **Set-ADUser** with the *-Replace* parameter to set the **ipPhone** attribute for the user.

1. Run the script and then verify that the **ipPhone** attribute is modified for the selected users.

## Exercise 3: Processing items by using If statements

Some of the servers in your organization have services that don't start properly when the server is restarted. You want to create a script that can be used to start a specified list of services. When you've performed sufficient testing, you plan to configure a scheduled task that runs the script. During the testing phase, you'll work with the Windows Time and Print Spooler services.

The main tasks for this exercise are:

1. Create services.txt with service names.
1. Create a script that starts stopped services.

### Task 1: Create services.txt with service names

1. On **LON-CL1**, open Windows PowerShell.
1. Create a new file **E:\\Mod07\\Labfiles\\services.txt**.
1. Identify the correct name for the **Print Spooler** service and add it to **services.txt**.
1. Identify the correct name for the **Windows Time** service and add it to **services.txt**.

### Task 2: Create a script that starts stopped services

1. Create a new script **E:\\Mod07\\Labfiles\\StartServices.ps1**.
1. Retrieve the service names from **services.txt** and place them in a variable.
1. Use a **ForEach** loop to process each service:

   - If the service isn't running, start it, and then enter text to the screen indicating that the service was started.
   - If the service is running, do nothing, and then enter text to the screen indicating that no action was required.

## Exercise 4: Creating users based on a CSV file

### Exercise scenario 4

The helpdesk for Adatum creates user accounts once per week based on data provided by the Human Resources department. This data is provided in a CSV file.

There have been multiple instances where the new user accounts weren't created with the correct information. The helpdesk has been using the CSV files as a reference and creating the user accounts by using graphical tools. You want to automate this process to avoid these errors.

The main task for this exercise is:

- Create AD DS users from a CSV file.

### Task 1: Create AD DS users from a CSV file

1. Create a new script named **E:\\Mod07\\Labfiles\\CreateUsers.ps1**.
1. Import **users.csv** and store the objects in a variable.
1. Create a **ForEach** loop that processes the data in the variable to create user accounts:

   - Create a variable that contains the Lightweight Directory Access Protocol (LDAP) name of the organizational unit for the user. For example: OU=IT,DC=Adatum,DC=com
   - Create a variable that contains the user principal name for the new user. This should be in the format **UserID@adatum.com**.
   - Create a variable that contains the display name for the new user. This should be in the format *FirstName LastName*.
   - Enter a status message to the screen indicating which user is being created and where.
   - Create the new user and be sure to set the following:

      - **GivenName**
      - **Surname**
      - **Name**
      - **DisplayName**
      - **SamAccountName**
      - **UserPrincipalName**
      - **Path**
      - **Department**

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

1. Perform all tasks using **LON-CL1**.
1. Identify the cmdlet that allows you to remotely query hardware information by using WS-MAN.
1. Identify the syntax required to query logical disk information and only include local disks.
1. Create a new script **E:\\Mod07\\QueryDisk.ps1**.
1. Add a **param()** block to the script that accepts a computer name and prompts for a computer name if one isn't provided.
1. Verify that the script correctly queries disk information from **LON-DC1**.

## Exercise 6: Updating the script to use alternate credentials

### Exercise scenario 6

You'd like to run a script that queries disk information from remote computers. To account for scenarios where the user doesn't have permission to query disk information on remote servers, you're updating the script to accept alternate credentials when specified.

The script needs to meet the following requirements:

- Accept a switch parameter to indicate whether alternate credentials are required.
- If alternate credentials are required, gather and use those credentials.

The main task for this exercise is:

- Update the script to use alternate credentials.

### Task 1: Update the script to use alternate credentials

1. Open **E:\\Mod07\\QueryDisk.ps1** for editing.
1. Update the **param()** block to include a switch that indicates alternate credentials will be used.
1. Add an **If** statement that evaluates the switch.

   - If the switch is true, run new code that gathers alternate credentials.
   - If the switch is false, run the existing query.

1. For new code, you must:
   - Get the credential from the user.
   - Open a remote session using that credential.
   - Send the query using that session.
