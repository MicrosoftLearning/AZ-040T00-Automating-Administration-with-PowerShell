# Copy the contents of this file into the scripting pane of the ISE. 
# Highlight one line and press F8 to execute just that line. 

# 1
Get-Process | Sort-Object –Property VM –Descending | Select-Object –First 10

# 2
Get-Date | Select-Object –Property DayOfWeek

# 3
Get-EventLog –Newest 10 –LogName Security | Select-Object –Property EventID,TimeWritten,Message

#4
Get-ADComputer -Filter * -Properties OperatingSystem | Sort -Property OperatingSystem | Select-Object -Property OperatingSystem,Name | fl -GroupBy OperatingSystem -Property Name

