# Open this file in the ISE. Highlight one line and press F8 to
# execute just that line. 

# 1
$dc = New-PSSession LON-DC1

# 2
Get-Module –PSSession $dc –ListAvailable

# 3
Import-Module –PSSession $dc –Name ActiveDirectory –Prefix Rem

# 4
Help Get-RemADUser
# and note that the server may not have updated help, so the help you get may be truncated and include only the Syntax section

# 5
Get-RemADUser –filter *

# 6
$dc | Remove-PSSession

# 7
Get-RemADUser 
# and note that an error is displayed because the command is no longer available through implicit Remoting.









