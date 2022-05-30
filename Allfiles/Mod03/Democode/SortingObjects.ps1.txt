# Copy the contents of this file into the scripting pane of the ISE. 
# Highlight one line and press F8 to execute just that line. 

# 1
Get-Process

# 2
Get-Process | Sort-Object –Property ID

# 3
Get-Service | Sort-Object –Property Status 
# point out that Stopped appears before Running because the property is stored as a number 
# internally, with zero (stopped) coming before 1 (running).

# 4
Get-Service | Sort-Object –Property Status -Descending

# 5
Get-EventLog –LogName Security –Newest 10

# 6
Get-EventLog –LogName Security –Newest 10 | Sort-Object –Property TimeWritten

# 7
Get-ADUser -Filter * | Sort-Object –Property SurName | fw -AutoSize





