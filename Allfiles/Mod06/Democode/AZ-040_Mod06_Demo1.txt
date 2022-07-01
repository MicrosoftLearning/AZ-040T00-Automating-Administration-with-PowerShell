#Assign a value to a variable and view its value in memory
$num1 = 5
$num1

$logFile = "C:\Logs\Log.txt"
$logFile

$service = Get-Service W32Time
$service

#Display variable contents within text
Write-Host "The log file location is $logFile"

#Display properties of an object stored in a variable
$service | Format-List *
$service.status
$service | Format-Table Name,Status

#View variables in memory
Get-Variable
Get-ChildItem Variable:

#View variable type
$num1.GetType()
$logFile.GetType()
$service.GetType()
$service | Get-Member

#Forcing a specific variable type
$num2 = "5"
[Int]$num3 = "5"
$num2.GetType()
$num3.GetType()

$date1 = "March 5, 2019 11:45 PM"
[DateTime]$Date2 = "March 5, 2019 11:45 PM"
$date1.GetType()
$date2.GetType()

#When Windows PowerShell cannot convert the value to the
#correct type and error occurs
[Int]$num4 = "Text that can't convert"

#When adding dissimilar variable types, Windows PowerShell
#attempts to convert them to be the same based on the type
#of the first variable.

#String plus integer
$num2 + $num3

#Integer plus string
$num3 + $num2

#Integer plus string that cannot be converted
$num3 + $logFile
