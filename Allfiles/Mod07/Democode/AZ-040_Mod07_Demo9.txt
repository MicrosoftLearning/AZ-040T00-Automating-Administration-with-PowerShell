Param (
    [string]$ComputerName
)

If ($ComputerName -eq $null) {
    Write-Host "A ComputerName is required."
} Else {
    Get-EventLog -LogName System -Newest 20 -ComputerName $ComputerName
}
