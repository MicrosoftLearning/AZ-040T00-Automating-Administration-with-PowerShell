#Use Get-Content to import data from a text file
Get-Content D:\Allfiles\Mod07\Democode\computers.txt
$computers = Get-Content D:\Allfiles\Mod07\Democode\computers.txt
$computers.count
$computers

#Use Import-Csv to import data from a .csv file
Import-Csv D:\Allfiles\Mod07\Democode\users.csv
$users = Import-Csv D:\Allfiles\Mod07\Democode\users.csv
$users.count
$users[0]
$users[0].First

#Use Import-Clixml to import data from an XML file
Import-Clixml D:\Allfiles\Mod07\Democode\users.xml
$usersXml = Import-Clixml D:\Allfiles\Mod07\Democode\users.xml
$usersXml.count
$usersXml[0]
$usersXml | Get-Member
