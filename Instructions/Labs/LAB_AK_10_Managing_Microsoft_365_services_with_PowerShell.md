---
lab:
    title: 'Lab: Managing Microsoft 365 with PowerShell'
    type: 'Answer Key'
    module: 'Module 10: Managing Microsoft 365 services with PowerShell'
---

# Lab answer key: Managing Microsoft 365 with PowerShell

## Exercise 1: Managing users and groups in Azure AD

### Task 1: Connect to Azure AD

1. On **LON-CL1**, select **Start**, and then enter **powersh**.
1. In the results list, right-click **Windows PowerShell** or activate its context menu, and then select **Run as administrator**.
1. To install the **AzureAD** module, in the **Administrator: Windows PowerShell** console, enter the following command, and then press the Enter key (when prompted for confirmation, enter **Y** and press the Enter key again twice in a row):

   ```powershell
   Install-Module AzureAD
   ```

1. To connect to Azure AD, enter the following command, and then press the Enter key:

   ```powershell
   Connect-AzureAD
   ```

1. In the **Sign in to your account** window, enter the name of the user account with the Global Administrator role in the Azure Active Directory (Azure AD) tenant you will be using in this lab, and then select **Next**.
1. At the **Enter password** prompt, enter your password, and then select **Sign in**.
1. To review a list of users in Azure AD, enter the following command, and then press the Enter key:

   ```powershell
   Get-AzureADUser
   ```

### Task 2: Create a new administrative user

1. To create a password profile object, in the **Administrator: Windows PowerShell** console, enter the following command, and then press the Enter key:

   ```powershell
   $PasswordProfile = New-Object -TypeName Microsoft.Open.AzureAD.Model.PasswordProfile
   ```

1. Identify an arbitrary but complex password that you want to use for a new user and record it since you will need it later in this lab. Make sure that the password is at least 8 characters-long, including a combination of lower case letters, upper case letters, digits, and at least one special character.
In the next step, replace `<password>` with the password you decided to use.
1. To set the password property of the password profile object, enter the following command, and then press the Enter key:

   ```powershell
   $PasswordProfile.Password = "<password>"
   ```

1. To create a new Azure AD user, enter the following commands, and then press the Enter key:

   ```powershell
   $verifiedDomain = (Get-AzureADTenantDetail).VerifiedDomains[0].Name
   New-AzureADUser -DisplayName "Noreen Riggs" -UserPrincipalName Noreen@$verifiedDomain -AccountEnabled $true -PasswordProfile $PasswordProfile -MailNickName Noreen
   ```

1. To store a reference to the new user object in a variable, enter the following command, and then press the Enter key:

   ```powershell
   $user = Get-AzureADUser -ObjectID Noreen@$verifiedDomain
   ```

1. To store a reference to the Global Administrator role in a variable, enter the following command, and then press the Enter key:

   ```powershell
   $role = Get-AzureADDirectoryRole | Where {$_.displayName -eq 'Global Administrator'}
   ```

1. To assign the Global Administrator role to Noreen's user account, enter the following command, and then press the Enter key:

   ```powershell
   Add-AzureADDirectoryRoleMember -ObjectId $role.ObjectId -RefObjectId $user.ObjectID
   ```

1. To verify that the Global Administrator role was assigned to Noreen's user account, enter the following command, and then press the Enter key:

   ```powershell
   Get-AzureADDirectoryRoleMember -ObjectId $role.ObjectId
   ```

1. In the output of the command, identify the **UserPrincipalName** attribute of Noreen's user account and record it. You will need it in one of the later exercises of this lab.

### Task 3: Create and license a new user

1. To create another Azure AD user, in the **Administrator: Windows PowerShell** console, enter the following command, and then press the Enter key:

   ```powershell
   New-AzureADUser -DisplayName "Allan Yoo" -UserPrincipalName Allan@$verifiedDomain -AccountEnabled $true -PasswordProfile $PasswordProfile -MailNickName Allan
   ```

1. To set the location property of the newly created user account, enter the following command, and then press the Enter key:

   ```powershell
   Set-AzureADUser -ObjectId Allan@$verifiedDomain -UsageLocation US
   ```

1. To review the available licenses in the tenant, enter the following command, and then press the Enter key:

   ```powershell
   Get-AzureADSubscribedSku | FL
   ```

1. To store the SKU ID for the intended license in a variable, enter the following command, and then press the Enter key:

   ```powershell
   $SkuId = (Get-AzureADSubscribedSku | Where SkuPartNumber -eq "ENTERPRISEPREMIUM").SkuID
   ```

1. To create an **AssignedLicense** object, enter the following command, and then press the Enter key:

   ```powershell
   $License = New-Object -TypeName Microsoft.Open.AzureAD.Model.AssignedLicense
   ```

1. To add the SKU ID to the license object, enter the following command, and then press the Enter key:

   ```powershell
   $License.SkuId = $SkuId
   ```

1. To create an **AssignedLicenses** object, enter the following command, and then press the Enter key:

   ```powershell
   $LicensesToAssign = New-Object -TypeName Microsoft.Open.AzureAD.Model.AssignedLicenses
   ```

1. To add the **AssignedLicense** object to the **AddLicenses** property, enter the following command, and then press the Enter key:

   ```powershell
   $LicensesToAssign.AddLicenses = $License
   ```

1. To configure Allan's user object with the **AssignedLicenses** object, enter the following command, and then press the Enter key:

   ```powershell
   Set-AzureADUserLicense -ObjectId Allan@$verifiedDomain -AssignedLicenses $LicensesToAssign
   ```

### Task 4: Create and populate a group

1. To review the existing groups, enter the following command, and then press the Enter key:

   ```powershell
   Get-AzureADGroup
   ```

1. To create a new security group, enter the following command, and then press the Enter key:

   ```powershell
   New-AzureADGroup -DisplayName "Sales Security Group" -SecurityEnabled $true -MailEnabled $false -MailNickName "SalesSecurityGroup"
   ```

1. To store a reference to Sales Security Group in a variable, enter the following command, and then press the Enter key:

   ```powershell
   $group = Get-AzureAdGroup -SearchString "Sales Security"
   ```

1. To store a reference to Allan Yoo's user account in a variable, enter the following command, and then press the Enter key:

   ```powershell
   $user = Get-AzureADUser -ObjectId Allan@$verifiedDomain
   ```

1. To add Allan Yoo's user account to the Sales Security Group, enter the following command, and then press the Enter key:

   ```powershell
   Add-AzureADGroupMember -ObjectId $group.ObjectId -RefObjectId $user.ObjectId
   ```

1. To verify that Allan Yoo's user account is a member of the Sales Security Group,  enter the following command, and then press the Enter key:

   ```powershell
   Get-AzureADGroupMember -ObjectId $group.ObjectId
   ```

1. In the output of the command, identify the **UserPrincipalName** attribute of Allan's user account and record it. You will need it in the next exercise.

## Exercise 2: Managing Exchange Online

### Task 1: Connect to Exchange Online

1. To install the **ExchangeOnlineManagement** module on **LON-CL1**, in the **Administrator: Windows PowerShell** console, enter the following command, and then press the Enter key (when prompted for confirmation, enter **A** and press the Enter key again):

   ```powershell
   Install-Module ExchangeOnlineManagement
   ```

1. To connect to Exchange Online, enter the following command, and then press the Enter key:

   ```powershell
   Connect-ExchangeOnline
   ```

1. In the **Sign in to your account** window, enter the name of the same user account you were using in the previous exercise of this lab, and then select **Next**.
1. At the **Enter password** prompt, enter your password, and then select **Sign in**.
1. To review a list of mailboxes in Exchange Online, enter the following command, and then press the Enter key:

   ```powershell
   Get-EXOMailbox
   ```

### Task 2: Create a room mailbox

1. To create a new room mailbox, in the **Windows PowerShell** console, enter the following command, and then press the Enter key:

   ```powershell
   New-Mailbox -Room -Name BoardRoom
   ```

1. To configure the new room to accept meeting requests, enter the following command, and then press the Enter key:

   ```powershell
   Set-CalendarProcessing BoardRoom -AutomateProcessing AutoAccept
   ```

### Task 3: Verify room resource booking

1. On **LON-CL1**, on the taskbar, select **Microsoft Edge**.
1. In Microsoft Edge, in the address bar, enter **https://outlook.office.com**, and then press the Enter key.
1. Sign in as Allan Yoo by using the UserPrincipalName as the user name and providing the password you recorded in the previous exercise of this lab. When prompted, change your password as instructed. Be sure to record the password so that you can use it during subsequent exercises.
1. If prompted to stay signed in, select **No**.
1. From the menu bar, select **Calendar**, and then select **New event**.
1. In the **Add a title** box, enter **Staff Meeting**.
1. In the **Invite attendees** box, enter **BoardRoom**, select **BoardRoom**, select the first available time, and then select **Send**.
1. From the menu, select **Mail**.
1. Verify that Allan has received a response from **BoardRoom** that the meeting request was accepted.
1. Sign out from Allan's user account.
1. Close Microsoft Edge.

## Exercise 3: Managing SharePoint Online

### Task 1: Connect to SharePoint Online

1. To install the SharePoint Online Management Shell, on **LON-CL1**, in the **Administrator: Windows PowerShell** console, enter the following command, and then press the Enter key (when prompted for confirmation, enter **A** and press the Enter key again):

   ```powershell
   Install-Module -Name Microsoft.Online.SharePoint.PowerShell
   ```

1. To connect to SharePoint Online, enter the following commands, and then press the Enter key:

   ```powershell
   $verifiedDomainShort = $verifiedDomain.Split(".")[0]
   Connect-SPOService -Url "https://$verifiedDomainShort-admin.sharepoint.com"
   ```

1. When prompted, sign in as Noreen Riggs and change your password as instructed. Be sure to record the password so that you can use it during subsequent exercises.
1. To list the existing SharePoint Online sites, enter the following command, and then press the Enter key:

   ```powershell
   Get-SPOSite
   ```

### Task 2: Create a new site

1. To review the available templates, in the **Windows PowerShell** console, enter the following command, and then press the Enter key:

   ```powershell
   Get-SPOWebTemplate
   ```

1. To create a new site, enter the following command, and then press the Enter key:

   ```powershell
   New-SPOSite -Url https://$verifiedDomainShort.sharepoint.com/sites/Sales -Owner noreen@$verifiedDomain -StorageQuota 256 -Template EHS#1 -NoWait
   ```

   > **Note:** Creating the site can take 10 minutes or longer. The **-NoWait** parameter performs this task asynchronously, so you don't need to wait for its completion. If you intend to wait, you can verify the status of the SharePoint site by entering the following command, and then pressing the Enter key:

   ```powershell
   Get-SPOSite | FL Url,Status
   ```

1. To disconnect from SharePoint Online, enter the following command, and then press the Enter key:

   ```powershell
   Disconnect-SPOService
   ```

## Exercise 4: Managing Microsoft Teams

### Task 1: Connect to Microsoft Teams

1. To install the Microsoft Teams PowerShell Module, in the **Administrator: Windows PowerShell** console, enter the following command, and then press the Enter key (when prompted for confirmation, enter **A** and press the Enter key again):

   ```powershell
   Install-Module MicrosoftTeams
   ```

1. To connect to Microsoft Teams, enter the following command, and then press the Enter key:

   ```powershell
   Connect-MicrosoftTeams
   ```

1. In the **Sign in to your account** window, select the **Use another account** option, enter the name of the user account with the Global Administrator role in the Azure Active Directory (Azure AD) tenant you were using in this lab, and then select **Next**.
1. To verify that there are no existing teams, enter the following command, and then press the Enter key:

   ```powershell
   Get-Team
   ```

### Task 2: Create a new team

1. To create a Sales team, in the **Windows PowerShell** console, enter the following command, and then press the Enter key:

   ```powershell
   New-Team -DisplayName "Sales Team" -MailNickName "SalesTeam"
   ```

1. To place the team information in a variable, enter the following command, and then press the Enter key:

   ```powershell
   $team = Get-Team -DisplayName "Sales Team"
   ```

1. To review the information about your team, enter the following command, and then press the Enter key:

   ```powershell
   $team | FL
   ```

1. Review the information about the Sales Team. Notice that **GroupId** is a unique identifier.
1. To add a user to the team, enter the following command, and then press the Enter key:

   ```powershell
   Add-TeamUser -GroupId $team.GroupId -User Allan@$verifiedDomain -Role Member
   ```

1. To review the team users, enter the following command, and then press the Enter key:

   ```powershell
   Get-TeamUser -GroupId $team.GroupId
   ```

   > **Note:** Notice that the user that created the team is an owner.

## Task 3: Verify access to the team

1. On **LON-CL1**, on the taskbar, select **Microsoft Edge**.
1. In Microsoft Edge, in the address bar, enter **https://teams.microsoft.com**, and then press the Enter key.
1. Sign in as Allan Yoo by using the UserPrincipalName as the user name and providing the password you changed earlier in this lab. 
1. When prompted to stay signed in, select **No**.
1. Close the **Bring your team together** window, and then verify that **Sales Team** is listed.
1. Select **New conversation**, enter **Prices are increasing 10% at month end**, and then press the Enter key.
1. Close Microsoft Edge.
