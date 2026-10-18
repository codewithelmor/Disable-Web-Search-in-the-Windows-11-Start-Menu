# Restore the Classic Right-Click Context Menu in Windows 11

Brings back the full legacy right-click menu as the default in File Explorer and on the desktop, so you no longer need to click "Show more options" first.

Works on Windows 11 Home and Pro.

## How It Works

Windows 11 loads the new compact context menu through a shell COM component. Creating an empty `InprocServer32` entry for that component's CLSID under the current user's hive makes the shell fall back to the classic menu.

| Scope | Registry Path |
|-------|---------------|
| Current user | `HKEY_CURRENT_USER\Software\Classes\CLSID\{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}\InprocServer32` |

| Value Name | Type | Data |
|------------|------|------|
| `(Default)` | `REG_SZ` | Empty (leave blank) |

## Quick Start (Windows Terminal)

Run in Windows Terminal, Command Prompt, or PowerShell. No elevation is needed.

**Enable the classic menu:**

```cmd
reg add "HKCU\Software\Classes\CLSID\{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}\InprocServer32" /f /ve
```

**Apply the change** by restarting Explorer:

```cmd
taskkill /f /im explorer.exe & start explorer.exe
```

Or sign out and back in, or reboot.

## Manual Method (Registry Editor)

1. Press `Win + R`, type `regedit`, and press Enter.
2. Navigate to `HKEY_CURRENT_USER\Software\Classes\CLSID`.
3. Right-click `CLSID` > **New** > **Key** and name it `{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}`.
4. Right-click the new key > **New** > **Key** and name it `InprocServer32`.
5. Select `InprocServer32`, then double-click the `(Default)` value in the right pane.
6. Leave **Value data** empty and click **OK**. The value will display as `(value not set)`, which is expected.
7. Restart Explorer or sign out and back in.

## PowerShell Script

```powershell
$path = "HKCU:\Software\Classes\CLSID\{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}\InprocServer32"

if (-not (Test-Path $path)) {
    New-Item -Path $path -Value "" -Force | Out-Null
}

Stop-Process -Name explorer -Force
```

Explorer restarts automatically after being stopped.

## Revert

Delete the CLSID key to return to the Windows 11 default menu:

```cmd
reg delete "HKCU\Software\Classes\CLSID\{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}" /f
```

Then restart Explorer:

```cmd
taskkill /f /im explorer.exe & start explorer.exe
```

## Deploying to Multiple Machines

This setting lives in the per-user hive, so deploy it in the user's context with any of the following:

- **Group Policy Preferences** (Registry item under User Configuration)
- **Microsoft Intune** (PowerShell script run in the user context)
- **Logon script** using the commands above

## Notes

- The setting applies per user. Each account that wants the classic menu needs the key created under its own `HKCU`.
- Without changing anything, you can open the classic menu for a single right-click with `Shift + Right-click` or `Shift + F10`.
- Major Windows feature updates may reset or change this behavior. Recheck after upgrading.
- Editing the registry carries risk. Consider exporting the key or creating a restore point before making changes.
