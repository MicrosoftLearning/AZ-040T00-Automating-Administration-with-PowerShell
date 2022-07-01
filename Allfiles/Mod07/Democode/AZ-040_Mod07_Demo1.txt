#Verify script location
Set-Location D:\Allfiles\Mod07\Democode
Get-ChildItem HelloWorld.ps1

#Run a script using a full path
D:\Allfiles\Mod07\Democode\HelloWorld.ps1

#Run a script fromt the current directory
HelloWorld.ps1
.\HelloWorld.ps1

#Set the execution policy
Get-ExecutionPolicy
Set-ExecutionPolicy Restricted
.\HelloWorld.ps1
Set-ExecutionPolicy Unrestricted