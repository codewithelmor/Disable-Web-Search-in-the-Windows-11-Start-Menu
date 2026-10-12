# Disable Web Search in the Windows 11 Start Menu

Turns off Bing/web suggestions in the Windows 11 Start menu search box. Local apps, files, and settings still appear in results.

Works on Windows 11 Home and Pro.

## How It Works

The `DisableSearchBoxSuggestions` registry policy tells the Windows shell not to show web suggestions in the search box.

| Scope | Registry Path |
|-------|---------------|
| Current user | `HKEY_CURRENT_USER\Software\Policies\Microsoft\Windows\Explorer` |
| All users | `HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Explorer` |

| Value Name | Type | Data |
|------------|------|------|
| `DisableSearchBoxSuggestions` | `REG_DWORD` | `1` = disabled, `0` or absent = enabled |

## Quick Start (Command Line)

Run in Command Prompt or PowerShell.

**Current user:**

```cmd
reg add "HKCU\Software\Policies\Microsoft\Windows\Explorer" /v DisableSearchBoxSuggestions /t REG_DWORD /d 1 /f
```

**All users** (requires an elevated prompt):

```cmd
reg add "HKLM\Software\Policies\Microsoft\Windows\Explorer" /v DisableSearchBoxSuggestions /t REG_DWORD /d 1 /f
```

**Apply the change** by restarting Explorer:

```cmd
taskkill /f /im explorer.exe & start explorer.exe
```

Or sign out and back in, or reboot.

## Manual Method (Registry Editor)

1. Press `Win + R`, type `regedit`, and press Enter.
2. Navigate to `HKEY_CURRENT_USER\Software\Policies\Microsoft\Windows`.
3. If the `Explorer` key does not exist, right-click `Windows` > **New** > **Key** and name it `Explorer`.
4. Inside `Explorer`, right-click > **New** > **DWORD (32-bit) Value** and name it `DisableSearchBoxSuggestions`.
5. Double-click the value and set **Value data** to `1`.
6. Restart Explorer or sign out and back in.

## PowerShell Script

```powershell
$path = "HKCU:\Software\Policies\Microsoft\Windows\Explorer"

if (-not (Test-Path $path)) {
    New-Item -Path $path -Force | Out-Null
}

New-ItemProperty -Path $path -Name "DisableSearchBoxSuggestions" `
    -PropertyType DWord -Value 1 -Force | Out-Null

Stop-Process -Name explorer -Force
```

Explorer restarts automatically after being stopped.

## Revert

Delete the value, or set it back to `0`:

```cmd
reg delete "HKCU\Software\Policies\Microsoft\Windows\Explorer" /v DisableSearchBoxSuggestions /f
```

Use `HKLM` instead of `HKCU` if you applied the machine-wide setting.

## Deploying to Multiple Machines

Use the same registry path and value with any of the following:

- **Group Policy Preferences** (Registry item)
- **Microsoft Intune** (PowerShell script or custom OMA-URI/registry configuration)
- **Startup or logon script** using the commands above

## Notes

- The older policy "Don't search the web or display web results in Search" (`ConnectedSearchUseWeb = 0` under `HKLM\SOFTWARE\Policies\Microsoft\Windows\Windows Search`) is largely ignored by the Windows 11 Start menu. Use `DisableSearchBoxSuggestions` instead.
- Major Windows feature updates may reset this setting. Recheck after upgrading.
- Editing the registry carries risk. Consider exporting the key or creating a restore point before making changes.
