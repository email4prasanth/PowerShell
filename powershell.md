- PowerShell commands naming convention is in the form of `VERB-NOUN`. 
[Approved Verbs for PowerShell Commands](https://learn.microsoft.com/en-us/powershell/scripting/developer/cmdlet/approved-verbs-for-windows-powershell-commands?view=powershell-7.4)
- Commands are available in 
   - PowerShell.
   - Snapins.
   - Module.


| Syntax      | Description |
| :----       |     ----:   |
| $PSVersionTable | Display PS version |
| Get-PSSnapin | commands in Snapin (for 1.0 v) |
| Get-PSSnapin -Registered |  commands in Registered Snapin |
| Get-Module | Available Modules |
| Get-Module -ListAvailable | List of Commands in Module |
| Import-Module -name TroubleshootingPack | Importing a module name|
| Get-Command -Module TroubleshootingPack | Get commands in the module |
| Get-Command -Name *log* | Commands that contain log |
| Get-Command -Name *log* -CommandType Cmdlet | Commands that contain log in Command Type Cmdlet |
| Get-Command -Name *log* -CommandType Cmdlet,Function | Commands that contain log in different Command Type
| Get-Command -Verb get -Noun *log* | To get Commands with naming convention |
| Get-Command -verb get -Noun *service* | To get Commands with naming convention |
| get-aduser -Filter * | Active Directory is not available so it wont work |
| $env:PSModulePath | Path where enviroment variables are stored |
| Get-Service | Display status of service |