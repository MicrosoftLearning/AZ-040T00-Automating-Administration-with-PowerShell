# Copy the contents of this file into the scripting pane of the ISE. 
# Highlight one line and press F8 to execute just that line. 

# 1
Get-Process -Name Notepad | Stop-Process

# 2
Get-Process -Name Notepad | Stop-Process –Name Notepad

