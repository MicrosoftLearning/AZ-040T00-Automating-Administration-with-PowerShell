#Use Read-Host to obtain user input
$days = Read-Host "Enter the number of days"
$days

#Use Get-Credential to obtain and store a credential
$cred = Get-Credential
$cred | Format-List
$cred | Export-Clixml -Path E:\Mod07\Democode\cred.xml
Get-Content E:\Mod07\Democode\cred.xml

#Use Out-Gridview to obtain a user selection
Get-ADComputer -Filter * | Out-GridView
$computer = Get-ADComputer -Filter * | Out-GridView -OutputMode Single
$computer
