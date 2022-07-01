# Open this file in the ISE. Highlight one line and press F8 to
# execute just that line. 

# 1
Invoke-CimMethod –ComputerName LON-DC1 –ClassName Win32_OperatingSystem –MethodName Reboot

# 2
Mspaint

# 3
Get-CimInstance –Class Win32_Process –Filter "Name='mspaint.exe'" | Invoke-CimMethod –Name Terminate



