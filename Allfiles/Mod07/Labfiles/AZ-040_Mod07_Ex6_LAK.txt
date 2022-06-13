param(
    [string]$ComputerName=(Read-Host "Enter computer name"),
    [switch]$AlternateCredential
)

If ($AlternateCredential -eq $true) {
    $cred = Get-Credential
    $session = New-CimSession -ComputerName $ComputerName -Credential $cred
    Get-CimInstance Win32_LogicalDisk -CimSession $session -Filter "DriveType=3"
} Else {
    Get-CimInstance Win32_LogicalDisk -ComputerName $ComputerName -Filter "DriveType=3"
}

 