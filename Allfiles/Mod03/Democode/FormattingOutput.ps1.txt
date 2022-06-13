# Copy the contents of this file into the scripting pane of the ISE. 
# Highlight one line and press F8 to execute just that line. 

# 1
Get-Service

# 2
Get-Service | Format-List -Property Name, Status

# 3
Get-ADComputer -Filter * -Properties OperatingSystem

# 4
Get-ADComputer -Filter * -Properties OperatingSystem | ft -Property Name, OperatingSystem

# 5
Get-ADUser -Filter *

# 6
Get-ADUser -Filter * | fw -AutoSize
