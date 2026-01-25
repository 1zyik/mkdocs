---
title: Powershell
description: This doc page covers tips and tricks you can use with windows powershell.
icon: material/powershell
---

# Windows Powershell Tips and Tricks

### Get list of all installed windows server optional features
``` ps1
Get-WindowsOptionalFeature -Online | where {$_.state -eq "Enabled"} | ft -Property featurename
```
???+ tip
    Since these are admin features, make sure to run this in an elevated window. <br/>
    You can also output to a file by pipeing result using below command
    ```
    | Out-File -FilePath "path\tofile.txt"
    ```

### How to kill a process
``` bash
taskkill /f /pid <pid>
```
???+ tip
    Make sure to find the pid using Task Manager and replace `<pid>` with the unique value. 

### Set time and date to specific time zone
``` ps1
Set-TimeZone -Name "Central Standard Time"
```
???+ tip
    This is an admin feature, run in elevated window. <br>
    Use `Get-TimeZone` to know which one you are currently set to.<br>
    Use `Get-TimeZone -ListAvailable` to get all possible time zones you can apply. 
