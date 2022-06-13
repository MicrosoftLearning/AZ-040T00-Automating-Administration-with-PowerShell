# Copy the contents of this file into the scripting pane of the ISE. 
# Highlight one line and press F8 to execute just that line. 

# 1 
New-ADGroup -Name HelpDesk -Path "ou=IT,dc=Adatum,dc=com" –GroupScope Global

# 2
New-ADUser -Name "Jane Doe" -Department "IT"

# 3
Add-ADGroupMember "HelpDesk" -Members "Lara","Jane Doe"

# 4
Get-ADGroupMember HelpDesk

Set-ADuser Lara -StreetAddress "1530 Nowhere Ave." -City "Winnipeg" -State "Manitoba" -Country "CA"

# 5
Get-ADPrincipalGroupMembership "Jane Doe"

# 6
Get-ADuser Lara -Properties StreetAddress,City,State,Country


