$freeSpace = 2GB

If ($freeSpace -le 5GB) {
    Write-Host “Free disk space is less than 5 GB”
} ElseIf ($freeSpace -le 10GB) {
    Write-Host “Free disk space is less than 10 GB”
} ElseIf ($freeSpace -le 20GB) {
    Write-Host “Free disk space is less than 20 GB”
} Else {
    Write-Host “Free disk space is more than 20 GB”
}
