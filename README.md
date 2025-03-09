# windows-cheat-sheet


# Settings

## Account

### Change local password (not pin)

Method #1 - Powershell
```powershell
$Passwort = Read-Host "Neues Passwort" -AsSecureString
Set-LocalUser -Name $env:UserName -Password $Passwort
```



<br><br>

### Change PIN
- Settings > Account > Sign-in Options > Change PIM
  - Maybe the option is grey out becauuse you are inside of an organisation. then click on the blue text and then yoo are able to change it.







<br><br>
________
________
<br><br>









# Bitlocker

## Restore from boot locking
- Sometimes when you start your it maybe asks you for entering recovery key. In this case login at aka.ms/myrecoverykey and go to your devices and there yoou can show your recovery key




<br><br>
<br><br>
___
<br><br>
<br><br>





## Windows Firewall

### Block all .exe recursvely in current dir
```cmd
@ setlocal enableextensions 
@ cd /d "%~dp0"

for /R %%a in (*.exe) do (

netsh advfirewall firewall add rule name="Blocked with Batchfile %%a" dir=out program="%%a" action=block

)
```
- You only need to allow for internet access outbound:
  - system32/svchost.exe
  - iSCSI-Service (TCP)
