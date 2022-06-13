# Open this file in the ISE. Highlight one line and press F8 to
# execute just that line. 

# 1
$s = New-CimSession –ComputerName LON-DC1

# 2
Get-CimInstance –CimSession $s –ClassName Win32_OperatingSystem

# 3
$s | Remove-CimSession





