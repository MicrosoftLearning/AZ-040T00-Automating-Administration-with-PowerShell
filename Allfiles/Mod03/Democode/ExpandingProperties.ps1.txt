# Copy the contents of this file into the scripting pane of the ISE. 
# Highlight one line and press F8 to execute just that line. 

# 1
Get-ADComputer –filter *

# 2
Get-Service –ComputerName (Get-ADComputer –filter *)

# 3
Get-ADComputer –Filter * | Get-Member

# 4
Help Get-Service –ShowWindow

# 5
Get-ADComputer –Filter * | Select-Object –Property Name

# 6
Get-ADComputer –Filter * | Select-Object –Property Name | Get-Member

# 7
Get-ADComputer –Filter * | Select-Object –ExpandProperty Name

# 8
Get-ADComputer –Filter * | Select-Object –ExpandProperty Name | Get-Member

# 9
(Get-ADComputer –Filter * | Select-Object –ExpandProperty Name)

# 10
Get-Service –ComputerName (Get-ADComputer –Filter * | Select-Object –ExpandProperty Name)


