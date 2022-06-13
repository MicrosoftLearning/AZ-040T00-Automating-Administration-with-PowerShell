#Module 10, Lab A
#
#Ex 1: Enable remoting on a client 
#
#Task 1
#
Set-ExecutionPolicy RemoteSigned

Enable-PSremoting

help *sessionconfiguration* 

Get-PSSessionConfiguration
#
#Task 2
#
Enter-PSSession –ComputerName LON-DC1

Install-WindowsFeature NLB

Exit-PSSession
#
#Task 3
#
Enter-PSSession –ComputerName LON-DC1

Enter-PSSession –ComputerName LON-CL1

Exit-PSSession
#
#Task 4
#
Enter-PSSession –ComputerName localhost

Notepad

Exit-PSSession
#
#
#Ex 2: Performing one-to-many remoting
#
#Task 1
#
Help *adapter*

Help Get-NetAdapter

Invoke-Command -ComputerName LON-CL1,LON-DC1 -ScriptBlock { Get-NetAdapter -Physical }
#
#Task 2
#
Get-Process | Get-Member

Invoke-Command -ComputerName LON-DC1 -ScriptBlock { Get-Process } | Get-Member
#