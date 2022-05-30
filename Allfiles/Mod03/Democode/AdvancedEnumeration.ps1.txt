# Copy the contents of this file into the scripting pane of the ISE. 
# Highlight one line and press F8 to execute just that line. 

# 1
Get-ItemProperty –Path HKCU:\Network\* | ForEach-Object –Process { Set-ItemProperty –Path $PSItem.PSPath –Name RemotePath –Value $PSItem.RemotePath.ToUpper() }

# 2
Get-ChildItem E:\ -Directory -recurse | Where Name -eq Democode | ForEach-Object  {$PSItem.CreateSubdirectory('Test')} | Select-Object FullName