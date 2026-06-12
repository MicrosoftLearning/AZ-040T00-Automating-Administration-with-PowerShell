# Copy the contents of this file into the scripting pane of the ISE or VS Code.
# Highlight one line and press F8 to execute just that line.

# 1
Get-Service | ForEach Name

# 2
Get-EventLog –List | Where Log –eq 'System' | ForEach Clear

