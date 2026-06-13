# Open this file in the ISE or VS Code. Highlight one line and press F8 to
# execute just that line.
# NOTE: PSScheduledJob and Get-EventLog are only available in Windows PowerShell 5.1.
# This demo must be run in a Windows PowerShell 5.1 console.

# 1
Import-Module PSScheduledJob
Get-Job | Remove-Job

# 2
$trigger = New-JobTrigger –Once –At (Get-Date).AddMinutes(2)

# 3
Register-ScheduledJob –Trigger $trigger –Name DemoJob –ScriptBlock { Get-EventLog –LogName Application }

# 4
Get-ScheduledJob | Select –Expand JobTriggers 
# notice the Time

# 5
Get-ScheduledJob 
# wait until after the time that was displayed in the previous step.

# 6
Get-Job

# 7
Receive-Job –Name DemoJob

# 8
Get-Job –Name DemoJob | Remove-Job







