param(
    [string]$ComputerName=(Read-Host "Enter computer name")
)

Get-CimInstance Win32_LogicalDisk -ComputerName $ComputerName -Filter "DriveType=3"


 