---
marp: true
author: Bruno Willian
theme: default
#class: invert 
size: 16:9
title: Connect to Dataverse through powershell
backgroundImage: url('https://github.com/brunotw/Documents/blob/main/Slide6.PNG?raw=true')
---
#  **Interact with Dataverse through** ``Powershell``

---
### With this quick tutorial will you learn how to interact with dataverse through powershell.
### You can run CRUD operations as well as updating system settings.

---
## Prerequisites
- Windows Management Framework (WMF) version 5.1 or later
```ps
# Check WMF version 
$Host 
Version: 5.1.19041.1682
```
- Module **Microsoft.Xrm.Data.PowerShell**
```ps
Install-Module Microsoft.Xrm.Data.PowerShell
```

---
## Create and test Connection
```powershell
# Generate connection using interactive login
$conn = Get-CrmConnection -InteractiveMode

# Generate WhoAmI request
$request = new-object Microsoft.Crm.Sdk.Messages.WhoAmIRequest

# Executing request
$conn.Execute($request)

# Dispose Connection
$conn.Dispose()
```

---
## Create Account
```ps
# Create Account - The code can also be inline
$accountId = New-CrmRecord `
-conn $conn `
-EntityLogicalName account `
-Fields @{"name"="account name";"overriddencreatedon"=[datetime]"2000-01-01"}
```
---
## Retrieve Account
```ps
$account = Get-CrmRecord `
-conn $conn `
-EntityLogicalName account `
-Id $accountId -Fields name, createdon
```

---
## Delete Account
```ps
# All three ways work
Remove-CrmRecord -conn $conn -CrmRecord $account
Remove-CrmRecord $account
Remove-CrmRecord -conn $conn -EntityLogicalName "account" -Id $accountId
```
Note: If you don't specify any value for the -conn parameter
it will by default try to use $Conn. If you have created the connection
with a different name i.e $Service you will have to **always** specify 
the -conn parameter

---
## Manipulate System Settings

```ps
# Retrieve system setttings 
Get-CrmSystemSettings # Omitting parameter names
Get-CrmSystemSettings -conn $conn 

# Update system settings
Set-CrmSystemSettings -conn $conn -GlobalHelpUrl https://www.bing.com
```
---
## Helpful Commands
```powershell
# Get all commands available for a specific module
Get-Command -Module Microsoft.Xrm.Data.Powershell

# Get Installed Modules
Get-InstalledModule
    #Filter by Name
    Get-InstalledModule *Microsoft*

# Get Command details - I found this command the be the most useful since it provides
# examples and detail parameters of the functions
Get-Help Get-CrmEntityRecordCount -Detailed
```

---
## Final thoughts
Well some of you may be thinking "Ok, but how's that helpful?".

I think automation is the key here. If you've worked with CI/CD before you are probably aware that you can automate pretty much anything. With that in mind, you can leverage those functions to ease repetitive/timeconsuming tasks. 

The command below may give you some insights. You will find functions that range from creating records to exporting solutions
```ps 
Get-Command -Module Microsoft.Xrm.Data.Powershell
```

---
## I hope you found this content somehow useful.

# Thank you







