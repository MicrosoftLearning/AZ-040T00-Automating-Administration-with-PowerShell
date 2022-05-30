Function TestScope {
    Write-Host "At the start of the function `$var is $var"
    Read-Host "Press a key to continue"
    $var = "function var"
    Write-Host "After definition in the function `$var is $var"
    Read-Host "Press a key to continue"
    Write-Host "The script scope can still be accessed in a function: $script:var"
    Read-Host
    Return($var)
}

$var = "Script var"
Write-Host "In script before the function `$var is $var"
Read-Host "Press a key to continue"

$functionVar=TestScope

Write-Host "In script after the function `$var is $var"
Read-Host "Press a key to continue"
Write-Host "The `$FunctionVar passed back is $functionVar"
