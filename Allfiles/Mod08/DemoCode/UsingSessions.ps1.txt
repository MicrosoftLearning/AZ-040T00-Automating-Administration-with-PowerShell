# Open this file in the ISE. Highlight one line and press F8 to
# execute just that line. 

# 1
$dc = New-PSSession –ComputerName LON-DC1

# 2
$all = New-PSSession –ComputerName LON-DC1,LON-CL1

# 3
Get-PSSession

# 4
$dc

# 5
Enter-PSSession –Session $dc


# 6
Get-Process

# 7
Exit-PSSession

# 8
$dc

# 9
Invoke-Command –Session $all –ScriptBlock { Get-Service | Where { $_.Status –eq 'Running' }}

# 10
$dc | Remove-PSSession

# 11
Get-PSSession

# 12
Get-PSSession | Remove-PSSession





