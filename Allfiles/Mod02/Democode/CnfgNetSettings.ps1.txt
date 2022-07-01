# Copy the contents of this file into the scripting pane of the ISE. 
# Highlight one line and press F8 to execute just that line. 

# 1
Test-Connection LON-DC1

# 2
Get-NetIPConfiguration

# 3
New-NetIPAddress -InterfaceAlias Ethernet -IPAddress 172.16.0.30 -PrefixLength 16

Remove-NetIPAddress -InterfaceAlias Ethernet -IPAddress 172.16.0.40

# 4
Set-DnsClientServerAddress -InterfaceAlias Ethernet -IPAddress 172.16.0.11

# 5
Remove-NetRoute -InterfaceAlias Ethernet -DestinationPrefix 0.0.0.0/0 -Confirm:$false

# 6
New-NetRoute -InterfaceAlias Ethernet -DestinationPrefix 0.0.0.0/0 -NextHop 172.16.0.2

#7
Get-NetIPConfiguration

#8
Test-Connection LON-DC1