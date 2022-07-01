Param(
    [string]$Path=(Read-Host "Enter a folder path"),
    [switch]$Recurse
) #end Param

#Query files in the path specified
$files=Get-ChildItem -Path $Path -File -Recurse:$Recurse -ErrorAction SilentlyContinue

#Calculate total file size
$size = 0
$sizeMB = 0

Foreach ($f in $files) {
    $size += $f.length
} # end ForEach
[int]$sizeMB = $size/1MB

#Display file information 
Write-Host "In $Path there are $($files.count) files"
If ($Recurse -eq $true) {
    Write-Host "Subfolders are included"
}
Write-Host "Total file size is $sizeMB MB"
