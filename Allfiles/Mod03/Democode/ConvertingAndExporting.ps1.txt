# Copy the contents of this file into the scripting pane of the ISE. 
# Highlight one line and press F8 to execute just that line. 

# 1
Get-Process | ConvertTo-HTML

# 2
Get-Process | ConvertTo-HTML | Out-File E:\Procs.html

# 3
Get-Process | ConvertTo-JSON > C:\Procs.json

# 4
Get-Service | ConvertTo-CSV | Out-File Serv.csv 
# or run 
Get-Service | Export-CSV E:\Serv.csv

# 5
Notepad E:\Serv.csv

# 6
Get-Service | Export-CliXML E:\Serv.xml

# 7
Notepad E:\Serv.xml



