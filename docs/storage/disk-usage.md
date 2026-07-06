# Speicherverbrauch und Speicherfresser anzeigen

## Kurzantwort
Unter Windows gibt es nativ bereits eine Speicherübersicht unter `Einstellungen > System > Speicher`.

Dort siehst du die Belegung pro Laufwerk nach Kategorien wie Apps, temporäre Dateien, Dokumente, Bilder und weitere Speicherfresser. Das ist gut für eine grobe Übersicht, ersetzt aber keinen interaktiven Ordnerbaum wie `ncdu`.

## Was Windows nativ kann

### Speicheranzeige in den Einstellungen
Für eine schnelle grafische Übersicht:
- Öffne `Einstellungen > System > Speicher`.
- Wähle bei Bedarf ein Laufwerk aus.
- Prüfe die Aufschlüsselung nach Kategorien wie Apps, temporäre Dateien, Dokumente und Bilder.

Microsoft beschreibt die Speicheransicht und die Aufschlüsselung pro Laufwerk hier: [Storage settings in Windows](https://support.microsoft.com/en-US/Windows/Experience/Storage-FileManagement/storage-settings-in-windows?utm_source=chatgpt.com).

| Funktion | Nativ in Windows? |
| --- | --- |
| Laufwerk-Auslastung anzeigen | Ja |
| Kategorien wie Apps, temporäre Dateien, Dokumente | Ja |
| Automatisch Speicher bereinigen mit Speicheroptimierung | Ja |
| Vollständiger Ordnerbaum mit Größen und Prozentbalken | Nein |
| Interaktives Drilldown wie `ncdu` | Nicht wirklich |

### Speicheroptimierung
Windows kann mit Speicheroptimierung automatisch Speicher freigeben, zum Beispiel über temporäre Dateien oder den Papierkorb.

Mehr dazu: [Manage drive space with Storage Sense](https://support.microsoft.com/en-US/Windows/Experience/Storage-FileManagement/manage-drive-space-with-storage-sense?utm_source=chatgpt.com).

## PowerShell
Mit PowerShell kannst du Größen technisch auswerten, auch wenn die Darstellung deutlich weniger komfortabel ist als bei spezialisierten Tools.

### Gesamtsumme unter einem Pfad
```powershell
Get-ChildItem C:\Users -Recurse -File -Force -ErrorAction SilentlyContinue |
Measure-Object -Property Length -Sum
```

Das summiert die Dateigrößen unter `C:\Users`.

### Einfache Hitliste für direkte Inhalte eines Laufwerks
```powershell
Get-ChildItem C:\ -Force | ForEach-Object {
    $size = if ($_.PSIsContainer) {
        (Get-ChildItem $_.FullName -Recurse -File -Force -ErrorAction SilentlyContinue |
            Measure-Object -Property Length -Sum).Sum
    } else {
        $_.Length
    }

    [pscustomobject]@{
        Path = $_.FullName
        SizeGB = [math]::Round(($size / 1GB), 2)
        Type = if ($_.PSIsContainer) { 'Directory' } else { 'File' }
    }
} | Sort-Object SizeGB -Descending | Format-Table -AutoSize
```

Damit bekommst du eine tabellarische Übersicht, welche direkten Ordner und Dateien unter `C:\` am meisten Platz belegen. Auf großen Laufwerken kann das spürbar dauern.

Die Microsoft-Dokumentation zu `Measure-Object` findest du hier: [Measure-Object](https://learn.microsoft.com/de-de/powershell/module/microsoft.powershell.utility/measure-object?view=powershell-7.6&utm_source=chatgpt.com).

## Microsoft Sysinternals DU
Wenn du ein Microsoft-Tool für die Konsole willst, ist `DU` von Sysinternals oft die praktischste native-nahe Ergänzung.

```cmd
du -l 1 C:\
```

Wichtig:
- `DU` ist ein Microsoft-Tool.
- `DU` ist nicht standardmäßig vorinstalliert.
- Du musst es separat herunterladen.

Download und Doku: [Disk Usage (DU)](https://learn.microsoft.com/de-de/sysinternals/downloads/du?utm_source=chatgpt.com).

## Externe Tools für echte Visualisierung
Wenn du wirklich sehen willst, was auf der gesamten Festplatte wie viel Speicher verbraucht, sind externe Tools meist die beste Wahl.

### WinDirStat
- Open Source
- klassische Baumansicht
- Treemap zur visuellen Größenverteilung

Projektseite: [WinDirStat](https://windirstat.net/?utm_source=chatgpt.com).

### WizTree
- sehr schnell, besonders auf NTFS
- liest die Master File Table aus
- gut für schnelle Speicherfresser-Analysen

Projektseite: [WizTree](https://www.diskanalyzer.com/?utm_source=chatgpt.com).

### TreeSize Free
- Explorer-ähnliche Oberfläche
- Ordnergrößen, Balken und teils grafische Auswertung
- gut für Nutzer, die lieber grafisch arbeiten

Projektseite: [TreeSize Free](https://www.jam-software.de/treesize?utm_source=chatgpt.com).

## Praktische Empfehlung
- Wenn keine Drittanbieter-Software erlaubt ist: nutze `Einstellungen > System > Speicher` plus PowerShell oder Sysinternals `DU`.
- Wenn du eine schnelle und tiefe Analyse willst: nimm `WizTree`.
- Wenn Open Source wichtig ist: nimm `WinDirStat`.
- Wenn du eine Explorer-nahe Oberfläche willst: nimm `TreeSize Free`.

## Fazit
Windows hat nativ eine brauchbare grobe Speicheranalyse, aber keinen wirklich komfortablen interaktiven Ordnerbaum mit Drilldown und Größenvisualisierung wie typische Linux-Tools.

Für eine echte Analyse der Speicherfresser auf der gesamten Festplatte brauchst du in der Praxis meist ein externes Tool.
