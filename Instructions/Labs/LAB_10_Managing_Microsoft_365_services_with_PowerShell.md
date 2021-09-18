---
lab:
    title: 'Lab: Managing Microsoft 365 with PowerShell'
    module: 'Module 10: Managing Microsoft 365 services with PowerShell'
---

# Lab: Managing Microsoft 365 with PowerShell

## Scenario

You've created a new Microsoft 365 tenant. As a new administrator, you want to try using PowerShell to manage some of the Microsoft 365 services before you start deploying them to users.

## Objectives

After completing this lab, you'll be able to:

- Manage users in Azure AD.
- Manage Exchange Online.
- Manage SharePoint Online.
- Manage Microsoft Teams.

## Estimated time: 60 minutes

## Lab Setup

Virtual machines: **LON-DC1** and **LON-CL1**

Username: **Adatum\\Administrator**

Password: **Pa55w.rd**

For this lab, you'll use the available virtual machine environment. Before you begin the lab, complete the following steps:

1. Open **LON-DC1** and sign in as **Adatum\\Administrator** with the password **Pa55w.rd**.
1. Repeat step 1 for **LON-CL1**.

> **Note**: This lab requires an Office 365 tenant and a user with Global Administrator permissions in that tenant.

## Exercise 1: Managing users and groups in Azure AD

### Exercise scenario 1

You need to make sure that you understand how to create and manage users. You're particularly interested in learning how to assign licenses to users. In this exercise, you'll create an administrative user and standard user. You'll also create and populate a group.

The main tasks for this exercise are:

1. Connect to Azure AD.
1. Create a new administrative user.
1. Create and license a new user.

### Task 1: Connect to Azure AD

1. On **LON-CL1**, open Windows PowerShell as an administrator.
1. Install the module that allows you to manage Azure AD.
1. Connect to Azure AD and sign in as your admin user.
1. To verify that you're connected, review a list of users in Azure AD.

### Task 2: Create a new administrative user

1. Create a new **PasswordProfile** object in a variable, and then populate the **password** property.
1. Note the password so that you don't forget it.
1. Create a new user using the **PasswordProfile** object with the following attributes:
   - Display name: **Noreen Riggs**
   - User principal name: **Noreen@yourdomain.onmicrosoft.com**
   - Account enabled
   - MailNickName: **Noreen**
1. Add **Noreen Riggs** to the Global Administrator role.
1. Use the **Get-AzureADDirectoryRoleMember** cmdlet to verify that **Noreen Riggs** is in the Global Administrator role.

### Task 3: Create and license a new user

1. Create a new user by using the **PasswordProfile** object with the following attributes:
   - Display name: **Allan Yoo**
   - User principal name: **Allan@yourdomain.onmicrosoft.com**
   - Account enabled
   - MailNickName: **Allan**
1. Set the usage location for Allan Yoo to **US**.
1. List the licenses SKUs available in your tenant.
1. Create an **AssignedLicense** object, and then configure the **SkuId** property with the *SkuID* value from the **ENTERPRISEPREMIUM** license in your tenant.
1. Create an **AssignedLicenses** object, and then place the **AssignedLicense** object in the **AddLicenses** property.
1. Use the **AssignedLicenses** object to assign a license to Allan Yoo.

### Task 4: Create and populate a group

1. List the groups in Azure AD.
2. Create a new group in Azure AD with the following attributes:
   - Display name: **Sales Security Group**
   - Security enabled: `$true`
   - Mail enabled: `$false`
   - Mail nickname: **SalesSecurityGroup**
3. Add Allan Yoo as a member of Sales Security Group.
4. Query the Sales Security Group membership to verify that Allan Yoo is a member.

## Exercise 2: Managing Exchange Online

### Scenario 2

In this exercise, you will create a new room mailbox and configure the resource booking properties to automatically accept meeting requests. You will also verify that the resource booking works as expected.

The main tasks for this exercise are:

1. Connect to Exchange Online.
1. Create a room mailbox.
1. Verify room resource booking.

### Task 1: Connect to Exchange Online

1. On **LON-CL1**, open Windows PowerShell as an administrator.
1. Install the module that allows you to manage Exchange Online.
1. Connect to Exchange Online and sign in as your admin user.
1. To verify that you're connected, review a list of mailboxes in Exchange Online.

### Task 2: Create a room mailbox

1. Create a new room mailbox named **BoardRoom**.
1. Configure the calendar processing for **BoardRoom** to automatically accept meeting requests.

### Task 3: Verify room resource booking

1. Open the Microsoft Edge browser and go to **https://outlook.office.com**.
2. Sign in as **Allan Woo**.
3. From the Calendar, create a new event and include **BoardRoom** as an attendee.
4. Select an available time and send the meeting invite.
5. In the Outlook Inbox, verify that you received a response that the meeting request was accepted.

## Exercise 3: Managing SharePoint Online

You're familiar with the web-based administrative console used for managing SharePoint Online. It serves your needs well, but you want to test the process for creating a site by using Windows PowerShell in case you ever want to automate the process.

The main tasks for this exercise are:

1. Connect to SharePoint Online.
1. Create a new site.

### Task 1: Connect to SharePoint Online

1. To clear cached credentials, close the **Windows PowerShell** console and then open Windows PowerShell as an administrator.
1. In the **Windows PowerShell** console, install the module that enables you to manage SharePoint Online.
1. Connect to SharePoint Online, and then sign in as **Noreen Riggs**.
1. To verify your connection, list the sites in your tenant.

### Task 2: Create a new site

1. In the **Windows PowerShell** console, review the list of templates available in SharePoint.
1. Create a new SharePoint site with the following settings:

   - Url: `https://yourdomain.sharepoint.com/sites/Sales`
   - Owner: `noreen@yourdomain.onmicrosoft.com`
   - Storage quote: **256**
   - Template: **EHS#1**

   > **Note:** It might take a few minutes for the command processing to complete.

1. Use **Get-SPOSite** to review the status of the new site.

   > **Note:** Creating the site can take 10 minutes or longer.

1. Disconnect from SharePoint Online.

## Exercise 4: Managing Microsoft Teams

The Sales department is interested in using Microsoft Teams for collaboration. To help them experiment with using Microsoft Teams, you'll create a team by using PowerShell. You'll then give access to Allan Yoo from the Sales department.

The main tasks for this exercise are:

1. Connect to Microsoft Teams.
1. Create a new team.
1. Verify access to the team.

### Task 1: Connect to Microsoft Teams

1. In the **Windows PowerShell** console, install the module that allows you to manage Microsoft Teams.
1. Connect to Microsoft Teams and sign in as your admin user.
1. To verify your connection, list the sites in your tenant.
1. Use the **Get-Team** cmdlet to verify that there are no existing teams.

### Task 2: Create a new team

1. Create a new team with following properties:

   - Display Name: **Sales Team**
   - MailNickName: **SalesTeam**

2. Add **Allan Yoo** as a user in **Sales Team**
3. List the users in Sales Team to verify that Allan Yoo was added.

   > **Note:** Notice that the user that created the team is an owner.

### Task 3: Verify access to the team

1. Open Microsoft Edge and go to **https://teams.microsoft.com**.
2. Sign in as Allan Yoo.
3. In the Sales Team, create a new conversation with the text, **Prices are increasing 10% at month end**.
