#1
$quantity = Read-Host "Query how many log entries?"
#2
Invoke-Command –ArgumentList $quantity –ComputerName LON-DC1 –ScriptBlock { Param($x) Get-EventLog –LogName Security –newest $x }
#3
Invoke-Command -ComputerName lon-dc1 -ScriptBlock {Get-EventLog -LogName Security –Newest $Using:quantity}





