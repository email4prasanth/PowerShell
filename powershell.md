- PowerShell commands naming convention is in the form of `VERB-NOUN`. 
[Approved Verbs for PowerShell Commands](https://learn.microsoft.com/en-us/powershell/scripting/developer/cmdlet/approved-verbs-for-windows-powershell-commands?view=powershell-7.4)
```
| Syntax      | Description |
| :---        |    :----:   |
| $PSVersionTable
| Get-PSSnapin
| Get-PSSnapin -Registered
| Get-Module
| Get-Module -ListAvailable
| Import-Module -name TroubleshootingPack
| Get-Module
| Get-Command -Module TroubleshootingPack
| Get-Command -Name *log*
| Get-Command -Name *log* -CommandType Cmdlet
| Get-Command -Name *log* -CommandType Cmdlet,Function
| Get-Command -Verb get -Noun *log*
| Get-Command -Verb get -Noun *log* -CommandType Cmdlet,Function
| Get-Command -Verb get -Noun *log* -CommandType Cmdlet
| Get-Command -Verb get -Noun *log*
| get-adusr -filter *
| get-aduser -filter *
| get-aduser -Filter *
| Get-Module
| Get-Module -ListAvailable
| $env:PSModulePath
| Get-Command -verb get -Noun *ser*
| Get-Command -verb get -Noun *service*
| Get-Service