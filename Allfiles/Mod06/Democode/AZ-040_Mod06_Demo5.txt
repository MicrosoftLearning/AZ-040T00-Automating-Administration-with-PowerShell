#Create a hash table of user names and their department
$users = @{"Lara"="IT";"Peter"="Managers";"Sang"="Sales"}

#Display the contents of the hash table
$users
$users.Lara

#Update a value in the hash table
$users.Sang = "Marketing"
$users

#Add an item to the hash table
$users.Add("Tia","Research")

#Remove an item from the hash table
$users.Remove("Sang")
$users

#Creating calculated properties uses a hash table
#Name and Expression are the required items
#You can shorten to n and e
$prop = @{n="Size(KB)";e={$_.Length/1KB}}
$prop
Get-ChildItem C:\Windows -File | Format-Table Name,Length
Get-ChildItem C:\Windows -File | Format-Table Name,$prop
