# Hyper-V-Manager starten

Damit der `Hyper-V-Manager` sauber startet, sollte `Hyper-V` vorher bereits aktiviert sein. Falls nötig, siehe [Hyper-V aktivieren](../setup/enable.md).

## Weg 1: Über Win + R
- `Win + R` drücken
- `virtmgmt.msc` eingeben
- mit `Enter` bestätigen

Damit startet der `Hyper-V-Manager`.

## Weg 2: Über das Startmenü
- `Start` öffnen
- nach `Hyper-V-Manager` suchen
- Anwendung starten

## Was im Hyper-V-Manager geprüft werden sollte
Wenn `Hyper-V` korrekt aktiv ist, sollte Folgendes möglich sein:

- der `Hyper-V-Manager` startet ohne Fehlermeldung
- dein lokaler Computername erscheint links im Manager
- rechts sind Aktionen wie `Neu`, `Virtueller Computer` und `Virtueller Switch-Manager` sichtbar

Das reicht für eine einfache Funktionsprüfung bereits aus.

## Kurze Minimal-Prüfung
1. `Win + R`
2. `virtmgmt.msc`
3. prüfen, ob der `Hyper-V-Manager` sauber startet

## Typisches Problem

### Der `Hyper-V-Manager` startet nicht
Prüfen:

- ob der Neustart nach der Aktivierung wirklich ausgeführt wurde
- ob `Hyper-V` im Feature-Status auf `Enabled` steht
- ob der Aktivierungsvorgang ohne Fehler durchlief
