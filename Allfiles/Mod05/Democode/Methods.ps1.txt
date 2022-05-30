# Open this file in the ISE. Highlight one line and press F8 to
# execute just that line. 

# 1
Get-WmiObject –ClassName Win32_Service | Get-Member #and explain that the Change() method is one member of the class.

# 2
Get-WmiObject -Class Win32_Service | Get-Member | Where Name -eq 'Change' | Format-List Name,Definition
Get-CimClass –Class Win32_Service | Select-Object –ExpandProperty CimClassMethods | Sort-Object -Property Name
#3
Get-CimClass –Class Win32_Service | Get-Member

# For the rest of this demonstration, follow the steps
# in the instructor manual




