# windows-cheat-sheet

## Windows Firewall

### Block all .exe recursvely in current dir
```cmd
@ setlocal enableextensions 
@ cd /d "%~dp0"

for /R %%a in (*.exe) do (

netsh advfirewall firewall add rule name="Blocked with Batchfile %%a" dir=out program="%%a" action=block

)
```
