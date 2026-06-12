# Open this file in the ISE or VS Code. Highlight one line and press F8 to
# execute just that line.
# NOTE: Get-WmiObject (step 1) is only available in Windows PowerShell 5.1.
# In PowerShell 7, use Get-CimInstance (steps 2-4) for all queries.

# 1
Get-WmiObject –Class Win32_Service

# 2
Get-CimInstance –ClassName Win32_Process

# 3
Get-CimInstance –ClassName Win32_LogicalDisk –Filter "DriveType=3"

# 4
Get-CimInstance –Query “SELECT * FROM Win32_NetworkAdapter"




