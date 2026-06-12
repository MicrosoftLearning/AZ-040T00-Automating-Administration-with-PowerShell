# Open this file in the ISE or VS Code. Highlight one line and press F8 to
# execute just that line.
# NOTE: Get-WmiObject (steps 1-2) is only available in Windows PowerShell 5.1.
# In PowerShell 7, use Get-CimInstance and Get-CimClass instead.

# 1
Get-WmiObject –ClassName Win32_Service | Get-Member #and explain that the Change() method is one member of the class.

# 2
Get-WmiObject -Class Win32_Service | Get-Member | Where Name -eq 'Change' | Format-List Name,Definition
Get-CimClass –Class Win32_Service | Select-Object –ExpandProperty CimClassMethods | Sort-Object -Property Name
#3
Get-CimClass –Class Win32_Service | Get-Member

# For the rest of this demonstration, follow the steps
# in the instructor manual




