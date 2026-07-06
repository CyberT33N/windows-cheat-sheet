# Hyper-V aktivieren

## Voraussetzungen
Vor der Aktivierung sollten diese Punkte erfüllt sein:

- `Windows 10/11 Pro`, `Enterprise` oder `Education`
- Hardware-Virtualisierung im `BIOS` oder `UEFI` aktiviert
- ein Benutzerkonto mit Administratorrechten

`Hyper-V` steht auf `Windows Home` standardmäßig nicht zur Verfügung.

## Schnellweg über Win + R

### 1. Windows-Features öffnen
- `Win + R` drücken
- `optionalfeatures.exe` eingeben
- mit `Enter` bestätigen

### 2. Hyper-V aktivieren
- in der Liste `Hyper-V` suchen
- den Haken bei `Hyper-V` setzen
- sicherstellen, dass die Unterpunkte ebenfalls ausgewählt sind
- auf `OK` klicken

Windows installiert dann die benötigten Komponenten.

### 3. Neustart ausführen
Wenn Windows dazu auffordert:

- Computer neu starten

Ohne Neustart ist `Hyper-V` oft noch nicht vollständig aktiv.

## Wenn `optionalfeatures.exe` einen Fehler zeigt
Falls bei der Aktivierung ein Fehler erscheint, kann `Hyper-V` auch direkt per `PowerShell` aktiviert werden.

### 1. PowerShell als Administrator starten
- `Start` öffnen
- nach `PowerShell` suchen
- Rechtsklick auf `Windows PowerShell`
- `Als Administrator ausführen`

### 2. Hyper-V aktivieren
```powershell
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V-All -All -NoRestart
```

Wenn der Befehl erfolgreich war, folgt der Neustart:

```powershell
Restart-Computer
```

## Aktivierung nach dem Neustart prüfen

### Variante A: Feature-Status prüfen
```powershell
Get-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V-All
```

Erwartet wird:

```text
State : Enabled
```

### Variante B: Grunddaten des Systems prüfen
```powershell
Get-ComputerInfo | Select-Object WindowsProductName, WindowsEditionId, OsBuildNumber, HyperVisorPresent | Format-List
```

Wichtig ist vor allem:

```text
HyperVisorPresent : True
```

## Typische Probleme

### Hyper-V lässt sich nicht aktivieren
Mögliche Ursachen:

- falsche Windows-Edition, zum Beispiel `Home`
- Virtualisierung ist im `BIOS` oder `UEFI` deaktiviert
- Aktivierung über `optionalfeatures.exe` ist fehlgeschlagen

Dann den `PowerShell`-Weg als Administrator verwenden.
