# Open this file in the ISE. Highlight one line and press F8 to
# execute just that line. 

# 1
Get-WmiObject –Class Win32_Service

# 2
Get-CimInstance –ClassName Win32_Process

# 3
Get-CimInstance –ClassName Win32_LogicalDisk –Filter "DriveType=3"

# 4
Get-CimInstance –Query “SELECT * FROM Win32_NetworkAdapter"




