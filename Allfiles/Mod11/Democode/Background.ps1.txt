# Open this file in the ISE. Highlight one line and press F8 to
# execute just that line.

# Enable remoting
Enable-PSRemoting 

# 1
Start-Job –ScriptBlock { Dir C:\ -Recurse } –Name LocalDir

# 2
Invoke-Command –ScriptBlock { Get-EventLog –LogName Security –Newest 100 } –ComputerName LON-CL1,LON-DC1 –JobName RemoteLogs

# 3
Get-Job

# 4
Get-Job –Name LocalDir | Stop-Job

# 5
Receive-Job  –Name LocalDir

# 6
Remove-Job –Name LocalDir

# 7
Wait-Job -Name RemoteLogs
Get-Job 

# 8
$id = Get-Job –Name RemoteLogs -IncludeChildJob | Where location -eq 'LON-DC1' | Select -ExpandProperty ID

# 9
Get-Job –ID $id | Receive-Job –Keep 

# 10
Receive-Job –Name RemoteLogs

# 11
Remove-Job –Name RemoteLogs









