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
1. To install the **AzureAD** module, in the **Administrator: Windows PowerShell** console, enter the following command, and then select Enter:

   ```powershell
   Install-Module AzureAD
   ```

1. To connect to Azure AD, enter the following command, and then select Enter:

   ```powershell
   Connect-AzureAD
   ```

1. In the **Sign in to your account** window, enter your username that has Global Administrator permissions, and then select **Next**.
1. At the **Enter password** prompt, enter your password, and then select **Sign in**.
1. To review a list of users in Azure AD, enter the following command, and then select Enter:

   ```powershell
   Get-AzureADUser
   ```

### Task 2: Create a new administrative user

1. To create a password profile object, in the **Windows PowerShell** console, enter the following command, and then select Enter:

   ```powershell
   $PasswordProfile = New-Object -TypeName Microsoft.Open.AzureAD.Model.PasswordProfile
   ```

1. Think of a password that you want to use for a new user and make a note of it so that you don't forget. In the next step, replace `<password>` with the password you thought of.
1. To set the password property of the password profile object, in the console, enter the following command, and then select Enter:

   ```powershell
   $PasswordProfile.Password = "<password>"
   ```

1. To create a new Azure AD user, in the console, enter the following command, and then select Enter:

   ```powershell
   New-AzureADUser -DisplayName "Noreen Riggs" -UserPrincipalName Noreen@yourdomain.onmicrosoft.com -AccountEnabled $true -PasswordProfile $PasswordProfile -MailNickName Noreen
   ```

1. To place the new user in a variable, in the console, enter the following command, and then select Enter:

   ```powershell
   $user = Get-AzureADUser -ObjectID Noreen@yourdomain.onmicrosoft.com
   ```

1. To place the Global Administrator role in a variable, in the console, enter the following command, and then select Enter:

   ```powershell
   $role = Get-AzureADDirectoryRole | Where {$_.displayName -eq 'Global Administrator'}
   ```

1. To assign Noreen to the global administrator role, in the console, enter the following command, and then select Enter:

   ```powershell
   Add-AzureADDirectoryRoleMember -ObjectId $role.ObjectId -RefObjectId $user.ObjectID
   ```

1. To verify that Noreen is added to the global administrator role, in the console, enter the following command, and then select Enter:

   ```powershell
   Get-AzureADDirectoryRoleMember -ObjectId $role.ObjectId
   ```

### Task 3: Create and license a new user

1. To create a new Azure AD user, in the **Windows PowerShell** console, enter the following command, and then select Enter:

   ```powershell
   New-AzureADUser -DisplayName "Allan Yoo" -UserPrincipalName Allan@yourdomain.onmicrosoft.com -AccountEnabled $true -PasswordProfile $PasswordProfile -MailNickName Allan
   ```

1. To set the location for the user, in the console, enter the following command, and then select Enter:

   ```powershell
   Set-AzureADUser -ObjectId Allan@yourdomain.onmicrosoft.com -UsageLocation US
   ```

1. To review the available licenses in the tenant, in the console, enter the following command, and then select Enter:

   ```powershell
   Get-AzureADSubscribedSku | FL
   ```

1. To place the SKU ID for the desired license in a variable, in the console, enter the following command, and then select Enter:

   ```powershell
   $SkuId = (Get-AzureADSubscribedSku | Where SkuPartNumber -eq "ENTERPRISEPREMIUM").SkuID
   ```

1. To create an **AssignedLicense** object, in the console, enter the following command, and then select Enter:

   ```powershell
   $License = New-Object -TypeName Microsoft.Open.AzureAD.Model.AssignedLicense
   ```

1. To add the SKU ID to the license object, in the console, enter the following command, and then select Enter:

   ```powershell
   $License.SkuId = $SkuId
   ```

1. To create an **AssignedLicenses** object, in the console, enter the following command, and then select Enter:

   ```powershell
   $LicensesToAssign = New-Object -TypeName Microsoft.Open.AzureAD.Model.AssignedLicenses
   ```

1. To add the **AssignedLicense** object to the **AddLicenses** property, in the console, enter the following command, and then select Enter:

   ```powershell
   $LicensesToAssign.AddLicenses = $License
   ```

1. To configure Allan with the **AssignedLicenses** object, in the console, enter the following command, and then select Enter:

   ```powershell
   Set-AzureADUserLicense -ObjectId Allan@yourdomain.onmicrosoft.com -AssignedLicenses $LicensesToAssign
   ```

### Task 4: Create and populate a group

1. To review the existing groups, in the console, enter the following command, and then select Enter:

   ```powershell
   Get-AzureADGroup
   ```

1. To create a new security group, in the console, enter the following command, and then select Enter:

   ```powershell
   New-AzureADGroup -DisplayName "Sales Security Group" -SecurityEnabled $true -MailEnabled $false -MailNickName "SalesSecurityGroup"
   ```

1. To put the Sales Security Group in a variable, in the console, enter the following command, and then select Enter:

   ```powershell
   $group = Get-AzureAdGroup -SearchString "Sales Security"
   ```

1. To put Allan Yoo in a variable, in the console, enter the following command, and then select Enter:

   ```powershell
   $user = Get-AzureADUser -ObjectId Allan@yourdomain.onmicrosoft.com
   ```

1. To add Allan Yoo as a member of Sales Security Group, enter the following command, and then select Enter:

   ```powershell
   Add-AzureADGroupMember -ObjectId $group.ObjectId -RefObjectId $user.ObjectId
   ```

1. To verify Allan Yoo is a member of Sales Security Group,  enter the following command, and then select Enter:

   ```powershell
   Get-AzureADGroupMember -ObjectId $group.ObjectId
   ```

## Exercise 2: Managing Exchange Online

### Task 1: Connect to Exchange Online

1. On **LON-CL1**, select **Start**, and then enter **powersh**.
1. In the results list, right-click **Windows PowerShell** or activate its context menu, and then select **Run as administrator**.
1. To install the **ExchangeOnlineManagement** module, in the **Administrator: Windows PowerShell** console, enter the following command, and then select Enter:

   ```powershell
   Install-Module ExchangeOnlineManagement
   ```

1. To connect to Exchange Online, enter the following command, and then select Enter:

   ```powershell
   Connect-ExchangeOnline
   ```

1. In the **Sign in to your account** window, enter your username, and then select **Next**.
1. At the **Enter password** prompt, enter your password, and then select **Sign in**.
1. To review a list of mailboxes in Exchange Online, enter the following command, and then select Enter:

   ```powershell
   Get-EXOMailbox
   ```

### Task 2: Create a room mailbox

1. To create a new room mailbox, in the **Windows PowerShell** console, enter the following command, and then select Enter:

   ```powershell
   New-Mailbox -Room -Name BoardRoom
   ```

1. To configure the new room to accept meeting requests, in the console, enter the following command, and then select Enter:

   ```powershell
   Set-CalendarProcessing BoardRoom -AutomateProcessing AutoAccept
   ```

### Task 3: Verify room resource booking

1. On **LON-CL1**, on the taskbar, select **Microsoft Edge**.
1. In Microsoft Edge, in the address bar, enter **https://outlook.office.com**, and then select Enter.
1. Sign in as Allan Woo and change your password as instructed. Be sure to note the password so that you can remember it for later exercises.
1. When prompted to stay signed in, select **No**.
1. From the menu bar, select **Calendar**, and then select **New event**.
1. In the **Add a title** box, enter **Staff Meeting**.
1. In the **Invite attendees** box, enter **BoardRoom**, select **BoardRoom**, select the first available time, and then select **Send**.
1. From the menu, select **Mail**.
1. Verify that Allan has received a response from **BoardRoom** that the meeting request was accepted.
1. Close Microsoft Edge.

## Exercise 3: Managing SharePoint Online

### Task 1: Connect to SharePoint Online

1. Close the Windows PowerShell console.

1. Select **Start**, and then enter **powersh**.

1. In the results list, right-click **Windows PowerShell** or activate its context menu, and then select **Run as administrator**.

1. To install the SharePoint Online Management Shell, in the **Windows PowerShell** console, enter the following command, and then select Enter:

   ```powershell
   Install-Module -Name Microsoft.Online.SharePoint.PowerShell
   ```

1. When prompted to trust the repository, enter **A**, and then select Enter.

1. To connect to SharePoint Online, in the console, enter the following command, and then select Enter:

   ```powershell
   Connect-SPOService -Url https://yourdomain-admin.sharepoint.com
   ```

1. Sign in as Noreen Riggs and change your password as instructed. Be sure to note the password so that you can remember it for later exercises.

1. To review the existing sites, in the console, enter the following command, and then select Enter:

   ```powershell
   Get-SPOSite
   ```

### Task 2: Create a new site

1. To review the available templates, in the **Windows PowerShell** console, enter the following command, and then select Enter:

   ```powershell
   Get-SPOWebTemplate
   ```

1. To create a new site, in the console, enter the following command, and then select Enter:

   ```powershell
   New-SPOSite -Url https://yourdomain.sharepoint.com/sites/Sales -Owner noreen@yourdomain.onmicrosoft.com -StorageQuota 256 -Template EHS#1
   ```

   > **Note:** It might take a few minutes for this command to complete processing.

1. To verify the status of the SharePoint site, in the console, enter the following command, and then select Enter:

   ```powershell
   Get-SPOSite | FL Url,Status
   ```

   > **Note:** Creating the site can take 10 minutes or longer. Don't wait for site creation to complete.

1. To disconnect from SharePoint Online, in the console, enter the following command, and then select Enter:

   ```powershell
   Disconnect-SPOService
   ```

## Exercise 4: Managing Microsoft Teams

### Task 1: Connect to Microsoft Teams

1. To install the Microsoft Teams PowerShell Module, in the **Windows PowerShell** console, enter the following command, and then select Enter:

   ```powershell
   Install-Module MicrosoftTeams
   ```

1. When prompted to trust the repository, enter **A**, and then select Enter.
1. To connect to Microsoft Teams, in the console, enter the following command, and then select Enter:

   ```powershell
   Connect-MicrosoftTeams
   ```

1. Sign in as your admin user. Notice that you can't use Noreen for this activity, because you need a Microsoft Teams license to create teams.
1. To verify that there are no existing teams, in the console, enter the following command, and then select Enter:

   ```powershell
   Get-Team
   ```

### Task 2: Create a new team

1. To create a Sales team, in the **Windows PowerShell** console, enter the following command, and then select Enter:

   ```powershell
   New-Team -DisplayName "Sales Team" -MailNickName "SalesTeam"
   ```

1. To place the team information in a variable, in the console, enter the following command, and then select Enter:

   ```powershell
   $team = Get-Team -DisplayName "Sales Team"
   ```

1. To review the information about your team, in the console, enter the following command, and then select Enter:

   ```powershell
   $team | FL
   ```

1. Review the information about the Sales Team. Notice that **GroupId** is a unique identifier.
1. To add a user to the team, in the console, enter the following command, and then select Enter:

   ```powershell
   Add-TeamUser -GroupId $team.GroupId -User Allan@yourdomain.onmicrosoft.com -Role Member
   ```

1. To review the team users, in the console, enter the following command, and then select Enter:

   ```powershell
   Get-TeamUser -GroupId $team.GroupId
   ```

   > **Note:** Notice that the user that created the team is an owner.

## Task 3: Verify access to the team

1. On **LON-CL1**, on the taskbar, select **Microsoft Edge**.
1. In Microsoft Edge, in the address bar, enter **https://teams.microsoft.com**, and then select Enter.
1. Sign in as Allan Yoo.
1. When prompted to stay signed in, select **No**.
1. Close the **Bring your team together** window, and then verify that **Sales Team** is listed.
1. Select **New conversation**, enter **Prices are increasing 10% at month end**, and then select Enter.
1. Close Microsoft Edge.
