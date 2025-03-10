# Windows Cheat Sheet



# Network

## WLAN

### Get mac address of wlan adapter

<details><summary>Click to expand..</summary>

Du kannst die MAC-Adresse deines WLAN-Adapters auf mehreren Wegen herausfinden. Hier sind zwei einfache Methoden:  

### **Methode 1: Über die Eingabeaufforderung (cmd)**  
1. **Drücke** `Windows + R`, gib `cmd` ein und **drücke Enter**.  
2. **Gib folgenden Befehl ein:**  
   ```sh
   ipconfig /all
   ```  
3. **Suche nach dem Eintrag** für den WLAN-Adapter. Dort findest du die **physikalische Adresse**, die wie `XX-XX-XX-XX-XX-XX` formatiert ist. Das ist die MAC-Adresse.  

### **Methode 2: Über die Netzwerkeinstellungen**  
1. **Drücke** `Windows + R`, gib `ncpa.cpl` ein und **drücke Enter**.  
2. **Klicke mit der rechten Maustaste** auf dein WLAN-Netzwerk und wähle **Status**.  
3. **Klicke auf "Details..."** – dort siehst du die **physikalische Adresse**.  

Fertig ✅



</details>












<br><br>
<br><br>
___
<br><br>
<br><br>



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
