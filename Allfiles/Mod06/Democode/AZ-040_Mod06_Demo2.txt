#Set the value for a variable
$logFile = "C:\Logs\log.txt"

#Test whether a variable contains specific text
$logFile.Contains("C:")
$logFile.Contains("D:")

#Insert text into a variable value
#Note that the original variable value is not modified
#Output must be caputured to update the value
$logFile.Insert(7,"\MyScript")
$logFile
$logFile=$logFile.Insert(7,"\MyScript")
$logFile

#Replace text in a variable value
$logFile.Replace(".txt",".htm")

#Split a string into parts based on a separator
$logFile.Split("\")
$logFile.Split("\") | Select -Last 1

#Convert a string to upper or lowercase
#Parentheses are required for a method even when
#no value is specified
$logFile.ToUpper()
$logFile.ToLower()



