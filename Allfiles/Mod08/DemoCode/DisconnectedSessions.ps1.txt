# Open this file in the ISE. Highlight one line and press F8 to
# execute just that line. 

# 1
$dc = New-PSSession –ComputerName LON-DC1

# 2
Disconnect-PSSession –Session $dc

# 3
Get-PSSession –ComputerName LON-DC1

# 4
Get-PSSession –ComputerName LON-DC1 | Connect-PSSession

# 5
$dc 
# confirm that the session is available

# 6
Remove-PSSession –Session $dc






