#Module 7, Lab A, Exercise 1, Task 1

$logPath = "C:\Logs\"
$logPath.GetType()
$logPath | Get-Member
$logFile = "log.txt"
$logPath += $logFile
$logPath
$logPath.Replace("C:","D:")
$logPath = $logPath.Replace("C:","D:")
$logPath

#Module 7, Lab A, Exercise 1, Task 2

$today = Get-Date
$today.GetType()
$today | Get-Member
$logFile = [string]$today.Year + "-" + $today.Month + "-" + $today.Day + "-" + $today.Hour + "-" + $today.Minute + ".txt"
$logFile
$cutOffDate = $today.AddDays(-30)
Get-ADUser -Properties LastLogonDate -Filter {LastLogonDate -gt $cutOffDate}

#Module 7, Lab A, Exercise 2, Task 1

$mktgUsers = Get-ADUser -Filter {Department -eq "Marketing"} -Properties Department
$mktgUsers.count
$mktgUsers[0]
$mktgUsers | Set-ADUser -Department "Business Development"
$mktgUsers | Format-Table Name,Department
Get-ADUser -Filter {Department -eq "Marketing"}
Get-ADUser -Filter {Department -eq "Business Development"}

#Module 7, Lab A, Exercise 2, Task 12

$computers="LON-SRV1","LON-SRV2","LON-DC1"
$computers.IsFixedSize
$computers.Add("LON-DC2")
$computers.Remove("LON-SRV2")
$computers

#Module 7, Lab A, Exercise 3, Task 1
$mailList=@{"Frank"="Frank@fabriakm.com";"Libby"="LHayward@contso.com";"Matej"="MSTaojanov@tailspintoys.com"}
$mailList
$mailList.Libby
$mailList.Libby="Libby.Hayward@contoso.com"
$mailList.Add("Stela","Stela.Sahiti")
$mailList.Remove("Frank")
$mailList





