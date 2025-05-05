# Windows Cheat Sheet


# Sleep

## Hibernate
- You can enable hibernate with
```powershell
powercfg /hibernate on
shuitdown /h
```











<br><br>
________
________
<br><br>






# Network

<details><summary>Click to expand..</summary>


   
## Testen von Netzlaufwerk-Abhängigkeiten lokal simulieren

<details><summary>Click to expand..</summary>

## Ziel:
Simuliere das Verhalten eines Netzlaufwerks lokal, ohne ein echtes Netzwerk aufzubauen.

## Hintergrund:
Dein Skript prüft explizit auf zwei Dinge:
1. **UNC-Pfad**: `$ScriptPath -like "\\*"` – Prüft, ob der Pfad des Skripts mit `\\` beginnt.
2. **Netzlaufwerk**: `(Get-CimInstance Win32_LogicalDisk ... | Where-Object {$_.DriveType -eq 4})` – Prüft, ob der Laufwerksbuchstabe den `DriveType 4` (Network Drive) hat.

Andere Methoden wie `subst` erzeugen typischerweise `DriveType 3` (Local Disk), was von deinem Skript nicht als Netzlaufwerk erkannt wird.

## So simulierst du es lokal:

### 1. Ordner erstellen
Erstelle einen Ordner auf deiner lokalen Festplatte, z. B. `C:\TestShare`.

### 2. Ordner freigeben:
- Rechtsklicke auf den Ordner `C:\TestShare`.
- Gehe zu `Eigenschaften` > `Freigabe` > `Erweiterte Freigabe...`.
- Aktiviere „Diesen Ordner freigeben“.
- Gib einen Freigabenamen ein (z. B. `TestShare`).
- Klicke auf `Berechtigungen` und stelle sicher, dass dein Benutzerkonto mindestens Leseberechtigung hat (standardmäßig hat „Jeder“ Leserechte).
- Bestätige mit OK. Der Netzwerkpfad ist nun `\\localhost\TestShare` (oder `\\COMPUTERNAME\TestShare`).

### 3. Als Netzlaufwerk verbinden (optional):
- Öffne den Explorer.
- Rechtsklicke auf "Dieser PC" > "Netzlaufwerk verbinden...".
- Wähle einen freien Laufwerksbuchstaben (z. B. `Z:`).
- Gib als Ordner `\\localhost\TestShare` ein.
- Klicke auf „Fertig stellen“.

### 4. Testen:
- Kopiere deine `setup.ps1`-Datei in den Ordner `C:\TestShare` (oder direkt auf das gemappte Laufwerk `Z:`).
- Führe das Skript von diesem Ort aus (z. B. `Z:\setup.ps1` oder `\\localhost\TestShare\setup.ps1`).
- Das Skript sollte nun erkennen, dass es von einem Netzlaufwerk (`DriveType 4` für `Z:` oder einem UNC-Pfad) ausgeführt wird und die entsprechende Logik ausführen.


</details>




</details>


























<br><br>
________
________
<br><br>






# Internet

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
