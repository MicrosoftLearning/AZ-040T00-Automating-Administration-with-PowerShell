#Place the current date in a variable
$date = Get-Date

#View date properties
$date
$date.Hour
$date.Minute
$date.Day
$date.DayOfWeek
$date.Month
$date.Year

#Add or subtract time from a date
$date.AddDays(100)
$date.AddDays(-60)

#Long and short formats
$date.ToLongDateString()
$date.ToShortDateString()
$date.ToLongTimeString()
$date.ToShortTimeString()
