$users = Get-ADUser -Filter {Department -eq "Marketing"}

Write-Host "Users to be modified: $($users.count)"

ForEach ($user in $users) {
    Write-Host "Modifying user: $($user.Name)"
    Set-ADUser $user -Department "Business Development" -WhatIf
}