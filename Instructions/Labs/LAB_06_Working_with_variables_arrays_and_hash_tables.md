---
lab:
    title: 'Lab: Using variables, arrays, and hash tables in PowerShell'
    module: 'Module 6: Working with variables, arrays, and hash tables'
---

# Lab: Using variables, arrays, and hash tables in PowerShell

## Scenario

You're preparing to create scripts to automate server administration in your organization. Before you begin, you want to practice working with variables, arrays, and hash tables.

## Objectives

After completing this lab, you'll be able to:

- Work with variable types.
- Use arrays.
- Use hash tables.

## Estimated time: 45 minutes

## Lab setup

Virtual machines: **AZ-040T00A-LON-DC1**, **AZ-040T00A-LON-SVR1**, and **AZ-040T00A-LON-CL1**

Username: **Adatum\\Administrator**

Password: **Pa55w.rd**

For this lab, you'll use the available virtual machine environment. Before you begin the lab, complete the following steps:

1. Open **LON-DC1** and sign in as **Adatum\\Administrator** with the password **Pa55w.rd**.
1. Repeat step 1 for **LON-SVR1** and **LON-CL1**.

## Exercise 1: Working with variable types

### Exercise scenario 1

You first plan to practice working with different types of variables.

The main tasks for this exercise are:

1. Use string variables.
1. Use DateTime variables.

### Task 1: Use string variables

1. On **LON-CL1**, open a Windows PowerShell prompt.
1. Create a variable `$logPath` that contains **C:\logs**\.
1. For `$logPath`, identify the type of variable and the available properties and methods.
1. Create a variable `$logFile` that contains **log.txt**.
1. Update `$logPath` to include the contents of `$logFile`.
1. Update the path stored in `$logPath` to use drive **D** instead of drive **C**.
1. Leave the Windows PowerShell prompt open for the next task.

### Task 2: Use DateTime variables

1. At the Windows PowerShell prompt, create a variable `$today` that contains today’s date.
1. For the variable `$today`, identify the type of variable and the available properties and methods.
1. Use the properties of `$today` to create a string in the format **Year-Month-Day-Hour-Minute.txt**, and store the value in `$logFile`.
1. Create a variable `$cutOffDay` that contains the date **30** days before today.
1. Use **Get-ADUser** to query user accounts that have signed in since `$cutOffDay`. Filter by using the **LastLogonDate** property.
1. Leave the Windows PowerShell prompt open for the next exercise.

## Exercise 2: Using arrays

### Exercise scenario 2

Now that you've practiced using different types of variables, you want to work with arrays.

The main tasks for this exercise are:

1. Use an array to update the department for users.
1. Use an array list.

### Task 1: Use an array to update the department for users

1. Query all Active Directory Domain Services (AD DS) users in the **Marketing** department and place them in a variable named `$mktgUsers`. Include the **Department** property in the results.
1. Use `$mktgUsers` to identify the number of users in the Marketing department.
1. Display the first user in `$mktgUsers` and verify that the **Department** property is listed.
1. Pipe the users in `$mktgUsers` to **Set-ADUser** and update the department to **Business Development**.
1. Review the **Department** attribute in `$mktgUsers` to check if it has been updated.
1. Query all AD DS users in the **Marketing** department to verify that there are none.
1. Query all AD DS users in the **Business Development** department and verify that it matches the previous count from the Marketing department.
1. Leave the Windows PowerShell prompt open for the next task.

### Task 2: Use an array list

1. Create an arraylist named `$computers` with the values **LON-SRV1**, **LON-SRV2**, and **LON-DC1**.
1. Verify that `$computers` doesn't have a fixed size.
1. Add **LON-DC2** to `$computers`.
1. Remove **LON-SRV2** from `$computers`.
1. Display the contents of `$computers`.
1. Leave the Windows PowerShell prompt open for the next exercise.

## Exercise 3: Using hash tables

### Exercise scenario 3

After using variables and arrays, you plan to practice working with hash tables. You want to learn how working with hash tables differs from arrays and array lists.

The main task for this exercise is:

- Use a hash table.

### Task 1: Use a hash table

1. Create a hash table named `$mailList` with the following users and email addresses:

   - User **Frank** with the email address **Frank@fabrikam.com**
   - User **Libby** with the email address **LHayward@contoso.com**
   - User **Matej** with the email address **MStojanov@tailspintoys.com**

1. Display the contents of `$mailList`.
1. Display the email address for **Libby**.
1. Update the email address for **Libby** to **Libby.Hayward@contoso.com**.
1. Add a new email address for **Stela**: **Stela.Sahiti@treyresearch.net**.
1. Review the count of items in `$mailList`.
1. Remove **Frank** from `$mailList`.
1. Verify that **Frank** is removed.
1. Close the Windows PowerShell prompt.
