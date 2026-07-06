# Security and Recovery

## Bitlocker

### Restore from boot locking
- Sometimes when you start your it maybe asks you for entering recovery key. In this case login at [aka.ms/myrecoverykey](https://aka.ms/myrecoverykey) and go to your devices and there yoou can show your recovery key

## Defender

### Scan folder
```shell
Start-MpScan -ScanType CustomScan -ScanPath "C:\Projects\development-platform\vs-code\extensions\vscode-symbols"
```

### Windows Firewall

#### Block all .exe recursvely in current dir
```cmd
@ setlocal enableextensions
@ cd /d "%~dp0"

for /R %%a in (*.exe) do (

netsh advfirewall firewall add rule name="Blocked with Batchfile %%a" dir=out program="%%a" action=block

)
```

You only need to allow for internet access outbound:
- system32/svchost.exe
- iSCSI-Service (TCP)
