# Copy the contents of this file into the scripting pane of the ISE. 
# Highlight one line and press F8 to execute just that line. 

# 1
New-ADObject -Name JohnSmithcontact -Type contact -DisplayName "John Smith (Contoso.com)"

# 2
Get-ADObject -Filter "ObjectClass -eq 'contact'"

# 3
Set-ADObject -Identity "CN=Lara Raisic,OU=IT,DC=Adatum,DC=com" -Description "Member of support team"

# 4
Get-ADUser Lara -Properties Description

# 5
Rename-ADObject -Identity "CN=Helpdesk,OU=IT,DC=Adatum,DC=com" -NewName SupportTeam

# 6
Get-ADGroup helpdesk


