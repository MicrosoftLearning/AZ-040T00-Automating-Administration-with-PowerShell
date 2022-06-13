#Place items into an array
$computers = "LON-DC1","LON-SRV1","LON-CL1"
$users = Get-ADUser -Filter *

#View the items in an array
$computers
$users
$users.count
$users[125]

#View propterties and methods for array items
$computers | Get-Member
$users | Get-Member
$users[125].UserPrincipalName

#Add an item to an array
$computers += "LON-SRV2"
$computers

#Create an ArrayList
[System.Collections.ArrayList]$usersList = Get-ADUser -Filter *
$usersList.IsFixedSize

#Remove an item from an ArrayList
$usersList.count
$usersList[125]
$usersList.RemoveAt(125)
$usersList.count
$usersList[125]
