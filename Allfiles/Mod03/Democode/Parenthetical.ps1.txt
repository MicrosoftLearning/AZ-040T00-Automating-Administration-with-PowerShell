# Copy the contents of this file into the scripting pane of the ISE or VS Code.
# Highlight one line and press F8 to execute just that line.

# 1
New-ADGroup “London Users” -GroupScope global

# 2
Get-ADGroup "London Users" | Add-ADGroupMember

# 3
Get-ADGroup "London Users" | Add-ADGroupMember -Members (Get-ADUser -Filter {City -eq 'London'})

# 4
Get-ADGroupMember “London Users”



