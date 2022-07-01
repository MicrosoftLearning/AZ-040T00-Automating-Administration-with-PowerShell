# STEP 3
# Run this script on LON-DC1

Register-PSSessionConfiguration –Name Adatum.HelpDesk –Path C:\HelpDesk.pssc –RunAsCredential ADATUM\Administrator –ShowSecurityDescriptorUI

# Provide password Pa$$w0rd
# Answer Yes to all prompts
# On permissions dialog:
#    Click Add
#    Enter HelpDesk
#    Click OK
#    Select the HelpDesk group
#    Click OK
#    Select Full permissions for the HelpDesk group
#    Click OK








