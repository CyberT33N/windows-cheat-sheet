# Netzlaufwerk-Abhängigkeiten lokal simulieren

## Ziel
Simuliere das Verhalten eines Netzlaufwerks lokal, ohne ein echtes Netzwerk aufzubauen.

## Hintergrund
Dein Skript prüft explizit auf zwei Dinge:
1. **UNC-Pfad**: `$ScriptPath -like "\\*"` - Prüft, ob der Pfad des Skripts mit `\\` beginnt.
2. **Netzlaufwerk**: `(Get-CimInstance Win32_LogicalDisk ... | Where-Object {$_.DriveType -eq 4})` - Prüft, ob der Laufwerksbuchstabe den `DriveType 4` (Network Drive) hat.

Andere Methoden wie `subst` erzeugen typischerweise `DriveType 3` (Local Disk), was von deinem Skript nicht als Netzlaufwerk erkannt wird.

## So simulierst du es lokal

### 1. Ordner erstellen
Erstelle einen Ordner auf deiner lokalen Festplatte, z. B. `C:\TestShare`.

### 2. Ordner freigeben
- Rechtsklicke auf den Ordner `C:\TestShare`.
- Gehe zu `Eigenschaften` > `Freigabe` > `Erweiterte Freigabe...`.
- Aktiviere "Diesen Ordner freigeben".
- Gib einen Freigabenamen ein (z. B. `TestShare`).
- Klicke auf `Berechtigungen` und stelle sicher, dass dein Benutzerkonto mindestens Leseberechtigung hat (standardmäßig hat "Jeder" Leserechte).
  - Der **Default** wird einfach sein, dass nur **Lesen** berechtigt ist. Das heißt, wenn du etwas **testen** möchtest, wie dass du ein **Netzwerklaufwerk** usw. erstellst, dann musst du die **Rechte ändern**. Setze hier einfach **Vollzugriff**.
- Bestätige mit OK. Der Netzwerkpfad ist nun `\\localhost\TestShare` (oder `\\COMPUTERNAME\TestShare`).

### 3. Als Netzlaufwerk verbinden (optional)
- Öffne den Explorer.
- Rechtsklicke auf "Dieser PC" > "Netzlaufwerk verbinden...".
- Wähle einen freien Laufwerksbuchstaben (z. B. `Z:`).
- Gib als Ordner `\\localhost\TestShare` ein.
- Klicke auf "Fertig stellen".

### 4. Testen
- Kopiere deine `setup.ps1`-Datei in den Ordner `C:\TestShare` (oder direkt auf das gemappte Laufwerk `Z:`).
- Führe das Skript von diesem Ort aus (z. B. `Z:\setup.ps1` oder `\\localhost\TestShare\setup.ps1`).
- Das Skript sollte nun erkennen, dass es von einem Netzlaufwerk (`DriveType 4` für `Z:` oder einem UNC-Pfad) ausgeführt wird und die entsprechende Logik ausführen.
