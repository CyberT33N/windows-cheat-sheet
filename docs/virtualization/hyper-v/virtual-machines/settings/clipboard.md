# Kopieren und Einfügen zwischen Host und VM

Damit du Inhalte vom Host-System in eine VM einfügen kannst, muss der erweiterte Sitzungsmodus korrekt aktiviert sein.

## Wo du das einstellst
Im `Hyper-V-Manager`:

1. Rechts auf `Hyper-V-Einstellungen`
2. Unter `Server`:
   - `Richtlinie für den erweiterten Sitzungsmodus`
   - Haken setzen bei `Erweiterten Sitzungsmodus zulassen`
3. Unter `Benutzer`:
   - `Erweiterter Sitzungsmodus`
   - Haken setzen bei `Erweiterten Sitzungsmodus verwenden, wenn verfügbar`

## Danach
- VM komplett schließen oder die Verbindung trennen
- VM erneut über `Verbinden` öffnen
- falls ein Dialog mit lokalen Ressourcen erscheint, dort `Clipboard` beziehungsweise die gewünschten Ressourcen zulassen

## Prüfen
- auf dem Host-System etwas kopieren
- in der VM einfügen

Wenn das Einfügen nicht funktioniert, die VM-Verbindung noch einmal vollständig schließen und erneut mit aktivem erweiterten Sitzungsmodus öffnen.
