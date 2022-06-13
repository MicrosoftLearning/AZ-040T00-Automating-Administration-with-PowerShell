# Copy the contents of this file into the scripting pane of the ISE. 
# Highlight one line and press F8 to execute just that line. 

# 1
Get-Service | Measure-Object

# 2
Get-ADUser -Filter * | Measure-Object

# 3
Get-Process | Measure-Object –Property VM –Sum –Average
