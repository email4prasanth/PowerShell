- PowerShell commands naming convention is in the form of `VERB-NOUN`. 
[Approved Verbs for PowerShell Commands](https://learn.microsoft.com/en-us/powershell/scripting/developer/cmdlet/approved-verbs-for-windows-powershell-commands?view=powershell-7.4)
- Commands are available in 
   - PowerShell.
   - Snapins.
   - Module.


| Syntax      | Description |
| :----       |     :----   |
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

#### Part-3 PSHelp
- PowerShell Help
- Updatable Help
- Parameters - Decides how the command let behaves `EX: Get-Service -Name BITS (Command parameters parameter values (Int32 or string or process))`
- Optional & Mandatory Parameters
- Parameter Values
- Positional & Named Parametes
- Examples

```
Get-Command
Get-Command -CommandType Cmdlet
Get-Command -CommandType Cmdlet *get*
```
- Syntax gives the Parameter sets how to display 
```
Get-Help Get-Service
Get-Help Get-Service -Online
Get-Help Get-Service -Full
Get-Service
Get-Service -Name BITS 
Get-Service -DisplayName 'AnyDesk Service'
Get-Service -DisplayName 'Background Intelligent Transfer Service'
```
- If we decide to use parameter say `-Name` we cannot combine with `-DisplayName` it will trough error this can be aware by checking syntax
- Some other command
```
Get-Help Get-TimeZone
Get-Help Set-TimeZone
Get-Command -CommandType Function *get*
Get-Help Get-TargetPort
```
- To get local services in the computer
```
Get-Service -ComputerName .
```
- To know the dependent service and cross check in the UI, Type `service.msc` right click on `Background Intelligent Transfer Service`, `Windows Remote Management` -- properties -- dependencies 
```
Get-Service -Name BITS -RequiredServices
Get-Service -Name WinRM -RequiredServices
```
#### Optional & Mandatory Parameters  
- Optional parameter can be idetified as `[parmeter parametervalue]` Ex:  Here parameter Name is optional.
- Mandatory parameter is not specified in [] Ex: Get-Service -DisplayName 'BitLocker Drive Encryption Service', here parameter DisplayName is mandatory.

#### Positional & Named Parametes
- Service -Name BITS or Service BITS.

#### Part-4 Cmdlets & Alias
- Compare command prompt syntax `Get-Help Get-Service -Full` and `Show-Command Get-Service` Get-service UI.
- we can get the serives domain controller `Get-Service -ComputerName dc1`.
- TO know available alias `Get-Command *alias*`. `Get-Alias` or `gal` give the predefined alias available in powershell. To create an alais `Get-Help New-Alias` for `Get-Alias` with name `ga` the syntax is `New-Alias -name ga -value Get-Alias`, Once the powershell is closed this alias will disappear to overcome this we need to use `PROFILE SCRIPT`.

#### Part-5 Variable and DataType
- Variables
- single and double quotes
- strings
- Integers

- Creation of variable EX: 
```
$Test1 = "This is my variable1"
New-Variable Test2 "This is my variable2"
New-Variable -Name Test3 -value "This is my variable3"
${test4 variable} = "test4" (if variable name contains space or special char ! @ # $ % ^ & * ( ) - _ = + \ | [ ] { } ; : / ? . > )
```
- To display the varable we can use `$Test` or `$test` or `echo $Test`.
- These variables are stored in various drive to display it 
```
Get-Command -CommandType Cmdlet *drive*
Get-Help Get-PSDrive (Gets drives in the current session)
Get-PSDrive (Display drives C,D,E and Aliaa, variable, cert drives)
```
- To enter in varable drive and get list

```
cd variable:
ls or Get-ChildItem
Get-Command *variable*
Get-Help Clear-Variable
Clear-Variable -Name Test
Remove-Variable Test
New-Variable delete "delete now" or $delete = "delete now"
Get-Variable -Name PWD
Set-Variable -Name del -Value "hello"
New-Variable -Name path -Value "c:
>> temp"
$temp = "this is variable"
$integer1 =10
$integer1
Get-Variable integer1
```

#### Single and Double quots use case
- single or double quotes are used to represent the text
- Single quaots are string literal,  Double Quotes are varible replacement 
```
  $a1 =  'hello'
  $b = 5
  '$a1 $b' output is $a1 $b
  "$a1 $b" output is hello 5
```
#### Data Types
- string - anything (text or number) present inside single or double quote.
- Integer - without quotes
```
5+5 = 10
"5"+6 = 56 (character will append)
5+"6" = 11 (left hand side will decide the operation here it is int)
"5+6" +7 = 5+67
```
- Usecase we can retrive the content in a notepad using
```
notepad (server 1, server 2, server 3)
$servers =  Get-Content C:\Users\email\OneDrive\Desktop\server.txt
$servers
```

#### Part-6 Regular Expressions
- It is a pattern of special character that match string in a search.
- It is cross platform like grep, unix, java, python, powershell.
- -match return true or false and $matches returns the string
```
"Its mine" -match '\w' - True
$Matches - I
"Its mine" -match '\w' - True
$Matches - Its
"Its mine" -match '\w*\s\w+' - True
$Matches - Its mine
"Its mine" -match '\d' - False
$Matches - I
```
- we can represent Regex in `[]` for repetitive usage
```
"its my life" -match '[\w+]' - True 
$Matches - i
"its my life" -match '[\w]+' - True 
$Matches - its
"its my life" -match '[\w\s]+' - True 
$Matches - its my life
"its my 18 life" -match '[\d]+'
$Matches - 18
"hey?this" -match '\w+\?' - True (in \? backslash is a escape character it will ignore the meaning and gives symbol)
$Matches - hey?
```
- UseCase, consider an email id with first and last name, numbers are not allowed
```
'marri.prasanth@gmail.com' -match '\w*\.\w+' - True
$Matches marri.prasanth 
To display gmail also
'marri.prasanth@gmail.com' -match '\w*\.\w+@gmail.com' -True
$Matches marri.prasanth@gmail.com
```
- The above will display numbers also since \w* includes digits also
```
'marri.4prasanth@gmail.com' -match '\w*\.\w+@gmail.com' - Ture
$Matches marri.4prasanth@gmail.com
'marri.4prasanth@gmail.com' -match '[a-z]*\.[a-z]+@gmail.com' - False
'marri.prasanth@gmail.com' -match '[a-z]*\.[a-z]+@gmail.com' - True
```

#### Part-7 RegEX
- Named Captures
- Split Operators
- Replace Operators
- Select String

- Use Named Capture get first name, last name and email id from a given email `marri.prasanth@gmail.com`
- use paranthesis () to capture the index
```
"marri.prasanth@gmail.com" -match "([a-z]+)\.([a-z]+)@gmail.com"
Name                           Value
----                           -----
2                              prasanth
1                              marri
0                              marri.prasanth@gmail.com
```
- To access the value use index `$Matches[2]` gives prasanth, replace the index values with names by using `?""` or `?''`
```
"marri.prasanth@gmail.com" -match "(?'firstname'[a-z]+)\.(?'lastname'[a-z]+)@gmail.com"
Name                           Value
----                           -----
lastname                       prasanth
firstname                      marri
0                              marri.prasanth@gmail.com
```
- To get email id 
```
"marri.prasanth@gmail.com" -match "(?'email'(?'firstname'[a-z]+)\.(?'lastname'[a-z]+)@gmail.com)"
Name                           Value
----                           -----
email                          marri.prasanth@gmail.com
lastname                       prasanth
firstname                      marri
0                              marri.prasanth@gmail.com
```
- Split and Replace operator
```
"hello how are you" -split '\s' output: hello, how, are, you
"hello how are you" -replace '\s','-' output: hello-how-are-you
'marri prasanth' -replace '([a-z]+)\s([a-z]+)', '$2, $1' - prasanth, marri
'marri prasanth' -replace '([a-z]+)\s([a-z]+)' '$2, $1' - no output comma should be used
```
