# Open this file in the ISE. Highlight one line and press F8 to
# execute just that line. 

# 1
Set-ExecutionPolicy RemoteSigned
Enable-PSRemoting
# If you get an error about a network connection being Public, 
# run Enable-PSRemoting –SkipNetwork instead. 
# Point out the error to students – it’s one they’ll see a lot.

# 2
Enter-PSSession –ComputerName LON-DC1

# 3
Get-Process

# 4
Exit-PSSession

# 5
Invoke-Command –ComputerName LON-CL1,LON-DC1 –ScriptBlock { Get-EventLog –LogName Security –Newest 10 }






