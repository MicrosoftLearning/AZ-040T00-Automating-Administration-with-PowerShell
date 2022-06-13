# ------------------------------------------------------------------------------------

$dc = New-PSSession -ComputerName LON-DC1

$dc

# ------------------------------------------------------------------------------------

Get-Module -ListAvailable -PSSession $dc

Get-Module -ListAvailable -PSSession $dc | Where { $_.Name -Like '*share*' }

Import-Module -PSSession $dc -Name SMBShare -Prefix DC

Get-DCSMBShare

Get-SmbShare

# ------------------------------------------------------------------------------------

Get-PSSession | Remove-PSSession








