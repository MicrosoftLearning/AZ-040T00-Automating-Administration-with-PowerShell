
# ------------------------------------------------------------------------------------

$computers = New-PSSession -ComputerName LON-CL1,LON-DC1

$computers

# ------------------------------------------------------------------------------------

Get-Module *security* –ListAvailable 

Invoke-Command -Session $computers -ScriptBlock { Import-Module NetSecurity }

Get-Command -Module NetSecurity

Invoke-Command -Session $computers -ScriptBlock { Get-NetFirewallRule -Enabled True } | Select Name,PSComputerName

Invoke-Command -Session $computers -ScriptBlock { Remove-Module NetSecurity }

# ------------------------------------------------------------------------------------

Get-WmiObject -Class Win32_LogicalDisk -Filter "DriveType=3"

Invoke-Command -Session $computers -ScriptBlock { Get-WmiObject -Class Win32_LogicalDisk -Filter "DriveType=3" }

Invoke-Command -Session $computers -ScriptBlock { Get-WmiObject -Class Win32_LogicalDisk -Filter "DriveType=3" } | ConvertTo-HTML -Property PSComputerName,DeviceID,FreeSpace,Size

# ------------------------------------------------------------------------------------

Get-PSSession | Remove-PSSession








