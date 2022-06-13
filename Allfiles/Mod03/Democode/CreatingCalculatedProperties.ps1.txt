# Copy the contents of this file into the scripting pane of the ISE. 
# Highlight one line and press F8 to execute just that line. 

# 1
Get-ADuser -Filter * -Properties whenCreated

# 2
Get-ADuser -Filter * -Properties whenCreated | Sort-Object -Property whenCreated -Descending

# 3
Get-ADUser -Filter * -Properties whenCreated | Sort-Object -Property whenCreated -Descending | Select-Object -Property Name,@{n='Account age (days)';e={(New-TimeSpan -Start $PSItem.whenCreated).Days}}

