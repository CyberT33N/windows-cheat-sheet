# Settings and Power

## Sleep

### Hibernate
You can enable hibernate with:

```powershell
powercfg /hibernate on
shuitdown /h
```

## Account

### Change local password (not pin)
Method #1 - Powershell

```powershell
$Passwort = Read-Host "Neues Passwort" -AsSecureString
Set-LocalUser -Name $env:UserName -Password $Passwort
```

### Change PIN
- Settings > Account > Sign-in Options > Change PIM
  - Maybe the option is grey out becauuse you are inside of an organisation. then click on the blue text and then yoo are able to change it.
