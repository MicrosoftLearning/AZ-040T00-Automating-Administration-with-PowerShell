# STEP 1
# Run this script on LON-CL1

New-ADGroup –Name HelpDesk –GroupScope Global –GroupCategory Security –SamAccountName HelpDesk

New-ADUser –Name HelpDeskTest –samAccountName HelpDeskTest

Set-ADAccountPassword –Identity HelpDeskTest –NewPassword (ConvertTo-SecureString –AsPlainText 'Pa$$w0rd' –force)

Add-ADGroupMember –Identity HelpDesk –Members HelpDeskTest

Enable-ADAccount HelpDeskTest






