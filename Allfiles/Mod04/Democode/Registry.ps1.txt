# Copy the contents of this file into the scripting pane of the ISE. 
# Highlight one line and press F8 to execute just that line. 

# 1
Set-Location HKLM:\Software

# 2
Get-ChildItem

# 3
New-Item -Name Demo

# 4
New-ItemProperty -path HKLM:\Software\Demo -Name Demo -Value Test -PropertyType String

#5
Get-ItemProperty -Path Demo
