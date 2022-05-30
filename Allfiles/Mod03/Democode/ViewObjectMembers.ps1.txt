# Copy the contents of this file into the scripting pane of the ISE. 
# Highlight one line and press F8 to execute just that line. 

# 1
Get-Service | Get-Member

# 2
Get-Process | Get-Member

# 3
Get-ChildItem | Get-Member

# 4
Get-ADUser -Filter * | Get-Member

# 5
Get-ADUser -Filter * -Properties *| Get-Member

