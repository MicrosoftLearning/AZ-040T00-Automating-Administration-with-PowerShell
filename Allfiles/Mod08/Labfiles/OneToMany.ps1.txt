# ------------------------------------------------------------------------------------

Help *adapter*

Help Get-NetAdapter

Invoke-Command -ComputerName LON-CL1,LON-DC1 -ScriptBlock { Get-NetAdapter -Physical }

# ------------------------------------------------------------------------------------

Get-Process | Get-Member

Invoke-Command -ComputerName LON-DC1 -ScriptBlock { Get-Process } | Get-Member

# ------------------------------------------------------------------------------------






