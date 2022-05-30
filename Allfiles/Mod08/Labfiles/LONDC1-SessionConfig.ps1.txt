# STEP 2
# Run this script on LON-DC1

New-PSSessionConfigurationFile –Path C:\HelpDesk.pssc –ExecutionPolicy Restricted –SessionType RestrictedRemoteServer –ModulesToImport ActiveDirectory –VisibleCmdlets Set-ADAccountPassword,ConvertTo-SecureString –LanguageMode FullLanguage






