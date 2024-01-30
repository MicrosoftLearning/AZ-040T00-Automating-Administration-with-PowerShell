---
lab:
    title: 'Lab: Managing Microsoft 365 with PowerShell'
    type: 'Answer Key'
    module: 'Module 10: Managing Microsoft 365 services with PowerShell'
---

# Lab answer key: Managing Microsoft 365 with PowerShell

## Exercise 1: Managing users and groups in Microsoft Entra ID

### Task 1: Connect to Microsoft Entra ID

Microsoft Graph PowerShell works with PowerShell 7 and later. It's also compatible with Windows PowerShell 5.1.

The following prerequisites are required to use the Microsoft Graph PowerShell SDK with Windows PowerShell.

- Upgrade to PowerShell 5.1 or later

The PowerShell script execution policy must be set to remote signed or less restrictive. Use Get-ExecutionPolicy to determine the current execution policy. For more information, see **[Install the Microsoft Graph PowerShell SDK](https://learn.microsoft.com/en-us/powershell/microsoftgraph/installation?view=graph-powershell-1.0)**.

1. On **LON-CL1**, select **Start**, and then enter **Windows PowerShell**.

1. In the results list, right-click **Windows PowerShell** or activate its context menu, and then select **Run as administrator**.

1. The PowerShell script execution policy must be set to remote signed or less restrictive, to set the execution policy, run the following command, and then type `A` and press the Enter key:

   ```powershell
   Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
   ```

1. To install the **Microsoft.Graph** module, in the **Administrator: Windows PowerShell** console, enter the following command, and then press the Enter key (when prompted for confirmation, type **Y** and press the Enter key again twice in a row):
   
   ```powershell
   Install-Module Microsoft.Graph -Scope CurrentUser
   ```

1. After the installation is completed, you can verify the installed version with the following command:

    ```powershell
   Get-InstalledModule Microsoft.Graph
   ```

1. To connect to Microsoft.Graph, enter the following command, and then press the Enter key:

   ```powershell
   # Using interactive authentication for users, groups, teamsettings.
   Connect-MgGraph -Scopes "User.ReadWrite.All", "Application.ReadWrite.All", "Sites.ReadWrite.All", "Directory.ReadWrite.All", "Group.ReadWrite.All", "TeamSettings.ReadWrite.All"
   ```

1. In the **Sign in to your account** window, enter the name of the user account with the Global Administrator role in the Microsoft Entra ID tenant you will be using in this lab, and then select **Next**.

1. At the **Enter password** prompt, enter your password, and then select **Sign in**.

1. To review a list of users in Azure AD, enter the following command, and then press the Enter key:

   ```powershell
   Get-MgUser
   ```

### Task 2: Create a new administrative user

1. To retrieve your organization's verified domain, in the **Administrator: Windows PowerShell** console, enter the following command, and then press the Enter key:

   ```powershell
   $verifiedDomain = (Get-MgOrganization).VerifiedDomains[0].Name
   ```

1. To create a password profile for the new user, enter the following command, and then press the Enter key:

   ```powershell
   $PasswordProfile = @{  
    "Password"="<password>";  
    "ForceChangePasswordNextSignIn"=$true  
   }  
   ```

   >**Note:** Identify an arbitrary but complex password that you want to use for a new user and record it since you will need it later in this lab. Make sure that the password is at least 8 characters-long, including a combination of lower case letters, upper case letters, digits, and at least one special character.
   In the next step, replace `<password>` with the password you decided to use.

1. To create a new Microsoft Entra ID user, enter the following commands, and then press the Enter key:

   ```powershell 
   New-MgUser -DisplayName "Noreen Riggs" -UserPrincipalName "Noreen@$verifiedDomain" -AccountEnabled -PasswordProfile $PasswordProfile -MailNickName "Noreen"
   ```

1. To store a reference to the new user ID in a variable, enter the following command, and then press the Enter key:

   ```powershell
   $user = Get-MgUser -UserId "Noreen@$verifiedDomain"
   ```

1. To store a reference to the Global Administrator role in a variable, enter the following command, and then press the Enter key:

   ```powershell
   $role = Get-MgDirectoryRole | Where {$_.displayName -eq 'Global Administrator'}
   ```

1. To assign the Global Administrator role to Noreen's user account, enter the following command, and then press the Enter key:

   ```powershell
   New-MgDirectoryRoleMemberByRef -DirectoryRoleId $role.id `
    -AdditionalProperties @{ "@odata.id" = "https://graph.microsoft.com/v1.0/directoryObjects/$user.id" }
   ```

1. To verify that the Global Administrator role was assigned to Noreen's user account, enter the following command, and then press the Enter key:

   ```powershell
   Get-MgDirectoryRoleMember -DirectoryRoleId $role.id
   ```

1. In the output of the command, identify the **UserPrincipalName** attribute of Noreen's user account and record it. You will need it in one of the later exercises of this lab.

### Task 3: Create and license a new user

1. To create another Azure AD user, in the **Administrator: Windows PowerShell** console, enter the following command, and then press the Enter key:

   ```powershell
   New-MgUser -DisplayName "Allan Yoo" -UserPrincipalName Allan@$verifiedDomain -AccountEnabled -PasswordProfile $PasswordProfile -MailNickName "Allan"
   ```

1. To set the location property of the newly created user account, enter the following command, and then press the Enter key:

   ```powershell
   Update-MgUser -UserId Allan@$verifiedDomain -UsageLocation US
   ```

1. To review the available licenses in the tenant, enter the following command, and then press the Enter key:

   ```powershell
   Get-MgSubscribedSku | FL
   ```

1. To store the SKU ID for the intended license in a variable, enter the following command, and then press the Enter key:

   ```powershell
   $SkuId = (Get-MgSubscribedSku | Where-Object { $_.SkuPartNumber -eq "ENTERPRISEPREMIUM" }).SkuId
   ```

1. To create an **AssignedLicense** object, enter the following command, and then press the Enter key:

   ```powershell
   $License = New-Object -TypeName PSCustomObject -Property @{
    DisabledPlans = @()
    SkuId = $SkuId
   }
   ```

1. To add the SKU ID to the license object, enter the following command, and then press the Enter key:

   ```powershell
   $License.SkuId = $SkuId 
   ```

1. To create an **AssignedLicenses** object, enter the following command, and then press the Enter key:

   ```powershell
   $LicensesToAssign = @(
    New-Object -TypeName PSCustomObject -Property @{
        DisabledPlans = @()
        SkuId = $SkuId
    }
   )
   ```

1. To add the **AssignedLicense** object to the **AddLicenses** property, enter the following command, and then press the Enter key:

   ```powershell
   $LicensesToAssign += $License
   ```

1. To configure Allan's user object with the **AssignedLicenses** object, enter the following command, and then press the Enter key:

   ```powershell
   Set-MgUserLicense -UserId Allan@$verifiedDomain -AddLicenses @{SkuId = $SkuId} -RemoveLicenses @()
   ```

### Task 4: Create and populate a group

1. To review the existing groups, enter the following command, and then press the Enter key:

   ```powershell
   Get-MgGroup
   ```

1. To create a new security group, enter the following command, and then press the Enter key:

   ```powershell
   New-MgGroup -DisplayName "Sales Security Group" -MailEnabled:$False  -MailNickName "SalesSecurityGroup" -SecurityEnabled
   ```

1. To store a reference to Sales Security Group in a variable, enter the following command, and then press the Enter key:

   ```powershell
   $group = Get-MgGroup -ConsistencyLevel eventual -Count groupCount -Search '"DisplayName:Sales Security"'
   ```

1. To store a reference to Allan Yoo's user account in a variable, enter the following command, and then press the Enter key:

   ```powershell
   $user = Get-MgUser -UserId Allan@$verifiedDomain
   ```

1. To add Allan Yoo's user account to the Sales Security Group, enter the following command, and then press the Enter key:

   ```powershell
   New-MgGroupMember -GroupId $group.id -DirectoryObjectId $user.id
   ```

1. To verify that Allan Yoo's user account is a member of the Sales Security Group,  enter the following command, and then press the Enter key:

   ```powershell
   Get-MgGroupMember -GroupId $group.id
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

1. In Microsoft Edge, in the address bar, enter `https://outlook.office.com`, and then press the Enter key.

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
   Get-Module -Name Microsoft.Online.SharePoint.PowerShell -ListAvailable | Select Name,Version
   Install-Module -Name Microsoft.Online.SharePoint.PowerShell -Scope CurrentUser
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
   Install-Module -Name MicrosoftTeams -Force -AllowClobber
   ```

1. To connect to Microsoft Teams, enter the following command, and then press the Enter key:

   ```powershell
   Connect-MicrosoftTeams
   ```

1. In the **Sign in to your account** window, select the **Use another account** option, enter the name of the user account with the Global Administrator role in the Microsoft Entra ID tenant you were using in this lab, and then select **Next**.

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

1. To retrieve your organization's verified domain, enter the following command, and then press the Enter key:

   ```powershell
   $verifiedDomain = (Get-MgOrganization).VerifiedDomains[0].Name
   ```

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

1. In Microsoft Edge, in the address bar, enter `https://teams.microsoft.com`, and then press the Enter key.

1. Sign in as Allan Yoo by using the UserPrincipalName as the user name and providing the password you changed earlier in this lab. 

1. When prompted to stay signed in, select **No**.

1. Close the **Bring your team together** window, and then verify that **Sales Team** is listed.

1. Select **New conversation**, enter **Prices are increasing 10% at month end**, and then press the Enter key.

1. Close Microsoft Edge.
