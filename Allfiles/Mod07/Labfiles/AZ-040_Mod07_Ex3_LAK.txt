$services = Get-Content services.txt

ForEach ($s in $services) {
    $status = (Get-Service $s).Status
    If ($Status -ne "Running") {
        Start-Service $s
        Write-Host "Started $s"
    } Else {
        Write-Host "$s is already started"
    }
}
