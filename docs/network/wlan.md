# WLAN

## Get mac address of wlan adapter

Du kannst die MAC-Adresse deines WLAN-Adapters auf mehreren Wegen herausfinden. Hier sind zwei einfache Methoden:

### Methode 1: Über die Eingabeaufforderung (cmd)
1. **Drücke** `Windows + R`, gib `cmd` ein und **drücke Enter**.
2. **Gib folgenden Befehl ein:**
   ```sh
   ipconfig /all
   ```
3. **Suche nach dem Eintrag** für den WLAN-Adapter. Dort findest du die **physikalische Adresse**, die wie `XX-XX-XX-XX-XX-XX` formatiert ist. Das ist die MAC-Adresse.

### Methode 2: Über die Netzwerkeinstellungen
1. **Drücke** `Windows + R`, gib `ncpa.cpl` ein und **drücke Enter**.
2. **Klicke mit der rechten Maustaste** auf dein WLAN-Netzwerk und wähle **Status**.
3. **Klicke auf "Details..."** - dort siehst du die **physikalische Adresse**.

Fertig.
