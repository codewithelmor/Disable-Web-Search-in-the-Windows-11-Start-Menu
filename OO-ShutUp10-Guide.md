# O&O ShutUp10: Comprehensive Guide

A practical guide to using **O&O ShutUp10** (also branded O&O ShutUp10++), a free privacy tool for Windows 10 and Windows 11 from O&O Software GmbH.

- **Product page:** https://www.oo-software.com/en/shutup10
- **Current version at time of writing:** 3.6.1135 (released 09/29/2026)
- **Supported systems:** Windows 10 and Windows 11
- **Price:** Free edition (portable); Premium edition (installed, paid)

---

## Table of Contents

1. [What It Is](#1-what-it-is)
2. [Why It Exists](#2-why-it-exists)
3. [Free vs. Premium](#3-free-vs-premium)
4. [Before You Start](#4-before-you-start)
5. [Getting and Launching the Tool](#5-getting-and-launching-the-tool)
6. [Understanding the Interface](#6-understanding-the-interface)
7. [Settings Categories](#7-settings-categories)
8. [Recommended Workflow](#8-recommended-workflow)
9. [Backup, Restore, and Undo](#9-backup-restore-and-undo)
10. [Exporting and Importing Profiles](#10-exporting-and-importing-profiles)
11. [Command-Line and Automated Deployment](#11-command-line-and-automated-deployment)
12. [Keeping Settings After Windows Updates](#12-keeping-settings-after-windows-updates)
13. [Trade-offs and What Can Break](#13-trade-offs-and-what-can-break)
14. [Troubleshooting](#14-troubleshooting)
15. [Related: Manual Registry Method for Web Search](#15-related-manual-registry-method-for-web-search)
16. [FAQ](#16-faq)
17. [Resources](#17-resources)

---

## 1. What It Is

O&O ShutUp10 gathers Windows privacy and convenience settings into a single window. Instead of hunting through Settings, Group Policy, and the registry, you flip switches in one list. It also labels each option with a recommendation so you can make informed choices without deep technical knowledge.

Key characteristics:

- **No installation (Free edition):** it runs directly as a portable executable.
- **No bundled extras:** the vendor states it installs no additional or unwanted software.
- **Around 300 settings** covering privacy and security.
- **Reversible:** individual changes can be undone, and restore points can be created.

## 2. Why It Exists

Windows is designed to be convenient and to ask users to confirm security notices as rarely as possible. A side effect is that more data may be sent to Microsoft than some users are comfortable with.

Much of that data powers personalization. For example, Windows can use calendar entries, email, location, and live traffic to suggest when to leave for the airport. Other convenience features carry real risks, such as logging typed input, sharing Wi-Fi access with contacts, or auto-connecting to open networks.

ShutUp10 lets you decide where convenience ends and privacy begins.

## 3. Free vs. Premium

| Capability | Free | Premium |
|---|:---:|:---:|
| Central management of privacy and system settings | ✓ | ✓ |
| Around 300 privacy/security settings | ✓ | ✓ |
| Restrict telemetry and diagnostics | ✓ | ✓ |
| Control app access to camera, mic, location, files | ✓ | ✓ |
| Search, cloud, and personalization controls | ✓ | ✓ |
| Copilot and Recall-related settings | ✓ | ✓ |
| Recommendation levels | ✓ | ✓ |
| One-click apply of recommended settings | ✓ | ✓ |
| Undo recommended settings | ✓ | ✓ |
| Editing mode for advanced users | ✓ | ✓ |
| Create and restore System Restore Points | ✓ | ✓ |
| Export/import profiles | ✓ | ✓ |
| Reset individual settings | ✓ | ✓ |
| Automatic reapplication after Windows updates | – | ✓ |
| Automatic restoration of changed settings | – | ✓ |
| Continuous background monitoring | – | ✓ |
| Client/service architecture | – | ✓ |
| No permanently required end-user admin rights | – | ✓ |
| Windows auto-restore notifications | – | ✓ |
| Portable, no installation | ✓ | – |
| Installed for permanent monitoring | – | ✓ |
| Cost | Free | From $14.90 (listed against a $19.90 regular price) |

**Choosing:**

- **Free** is the right fit if you are comfortable re-checking your settings after major Windows updates.
- **Premium** suits anyone who wants settings enforced continuously, or who manages machines where users should not need admin rights to keep settings in place.

Pricing is as shown on the vendor's editions page at the time of writing and may change.

## 4. Before You Start

1. **Create a System Restore Point.** The tool can do this for you (see [Section 9](#9-backup-restore-and-undo)).
2. **Use an administrator account.** Changing system-wide settings requires elevation.
3. **Know your goals.** Decide whether you want strict privacy, a balanced setup, or just to remove ads and suggestions.
4. **Note which features you rely on.** Location, voice input, cloud sync, and OneDrive integration are common casualties of aggressive settings.
5. **Check Windows edition and build.** Available options differ between Windows 10 and Windows 11, and between builds.

## 5. Getting and Launching the Tool

1. Go to the [official product page](https://www.oo-software.com/en/shutup10) and use the **Download for free** button.
2. Save the executable somewhere you will find it again (for example `C:\Tools\`).
3. Double-click to launch. Approve the UAC prompt.
4. No setup wizard is involved in the Free edition.

**Package manager option:** the package is also available through Chocolatey under the name `shutup10`:

```powershell
choco install -y shutup10
```

After a package-manager install, the executable is typically invoked as `OOSU10.exe`.

> Always download from the official O&O Software site or a trusted package source. Privacy tools are an attractive target for impersonation.

## 6. Understanding the Interface

The main window is a list of settings, grouped by topic. Each entry has:

- **A toggle switch:** on means the setting is applied (the data sharing or feature is restricted); off means Windows default behavior.
- **A recommendation label:** typically shown with color coding, indicating how strongly the tool suggests changing it.
- **A description:** explains what the setting does and what you lose by changing it. Read these before toggling anything.

The **Actions** menu provides bulk operations such as applying recommended settings, applying all settings, or undoing changes. Other menu items cover profile import/export and restore points.

### Recommendation levels

Settings are labeled by recommendation level, so you can apply the safe ones broadly and review the rest individually. A reasonable approach:

| Level | How to treat it |
|---|---|
| Recommended | Generally safe to enable for most users |
| Limited / conditionally recommended | Enable only if you understand the trade-off |
| Not recommended | Leave alone unless you have a specific reason |

### Editing mode

Advanced users can use the editing mode for finer control. Treat it as a power-user feature: confirm what each option does before applying it.

## 7. Settings Categories

The vendor's feature overview groups the available controls as follows.

### Privacy and telemetry

- Restrict telemetry and diagnostic data transfer.
- Disable the advertising ID and personalized advertising.
- Adjust feedback and diagnostic reporting.
- Turn off online speech recognition and personalization.
- Reduce suggestions, tips, and ad-style content.

### Apps and background activity

- Control which apps may run in the background.
- Restrict app access to contacts, calendar, email, and messages.
- Control access to microphone, camera, and location.
- Limit access to the file system, pictures, documents, and libraries.
- Limit access to motion data, Bluetooth, Wi-Fi, and device information.

### Location, sensors, and device access

- Disable or restrict location services.
- Manage location history and location-based features.
- Limit sensor access.
- Reduce transmission of device and usage information.

### Windows Search, cloud, and personalization

- **Disable Bing and web search in Windows Search.**
- Reduce search and input personalization.
- Restrict cloud-based content in Start, search, and widgets.
- Reduce Microsoft suggestions and recommendations.

### Cortana, voice, and online services

- Disable Cortana features where present.
- Restrict online services used for voice and text input.
- Reduce personalization through Microsoft services.

### Updates, reboots, and recommendations

- Adjust update-related comfort features.
- Reduce automatic app recommendations and suggested installs.
- Limit notices, tips, and suggestions.
- Review features Microsoft may re-enable after updates.

### Security and network

- Restrict automatic connection to open or public hotspots.
- Reduce network-related telemetry and sharing.
- Limit transfer of usage data to Microsoft services.

### OneDrive and Microsoft account integration

- Reduce OneDrive alerts and overlays.
- Restrict cloud-related synchronization (varies by Windows system).
- Reduce the connection between the local system and Microsoft services.

### Copilot and Recall

Both editions include settings related to Copilot and Recall on supported Windows 11 systems.

## 8. Recommended Workflow

1. **Create a restore point** from within the tool.
2. **Apply the recommended settings** using the one-click option as a baseline.
3. **Reboot** so all changes take effect.
4. **Use your PC normally for a few days.** Note anything that stops working.
5. **Tighten selectively.** Go through the "limited" and "not recommended" items one category at a time, reading each description.
6. **Export your profile** once you are happy (see [Section 10](#10-exporting-and-importing-profiles)).
7. **Re-check after major Windows updates**, or use Premium to automate this.

### Suggested profiles

| Profile | Approach |
|---|---|
| **Balanced** | Apply recommended settings only |
| **Privacy-focused** | Recommended settings plus selected limited-recommendation items (search, ads, suggestions, location) |
| **Locked down** | Selected additional options, accepting reduced convenience; test thoroughly |

## 9. Backup, Restore, and Undo

The tool offers several layers of safety:

- **System Restore Points:** create one before making changes, and restore it if something goes wrong.
- **Undo recommended settings:** reverts the recommended set in one action.
- **Reset individual settings:** toggle a single option back to its default.
- **Profile export:** keep a snapshot of a known-good configuration.

**Best practice:** make a restore point before large changes, especially before applying anything beyond the recommended set.

If System Restore is disabled on your machine, enable it in **System Properties > System Protection** first.

## 10. Exporting and Importing Profiles

Your chosen configuration can be saved to a file and applied on other machines.

**Export:**
1. Configure the tool the way you want.
2. Use the export option in the menu and save the `.cfg` file.

**Import:**
1. Launch the tool on the target machine.
2. Use the import option and select the `.cfg` file.

Profiles are plain text. Each setting is identified by a short code and marked with a `+` (enabled) or `-` (disabled), which makes them easy to review, version, and share.

```
# Example format (illustrative only)
P017 +
W001 +
M006 -
```

Keep a copy of your profile in cloud storage or version control so you can rebuild your setup after a reinstall.

## 11. Command-Line and Automated Deployment

A saved profile can be applied without opening the interface, which is useful for scripts and deployment tools.

**Basic import:**

```cmd
OOSU10.exe "C:\Path\To\ooshutup10.cfg"
```

**Silent import (closes immediately after import with no feedback):**

```cmd
OOSU10.exe "C:\Path\To\ooshutup10.cfg" /quiet
```

The `/quiet` option is documented in the header comments of profiles exported by the tool. Community deployment scripts also pass a `/force` switch together with `/quiet`; check the vendor documentation for the behavior in your version before relying on it.

**Example PowerShell deployment:**

```powershell
# Run elevated
$cfg = "C:\Deploy\ooshutup10.cfg"
& "C:\Deploy\OOSU10.exe" $cfg /quiet
```

**Common deployment scenarios:**

- **Imaging/OS build:** post-install steps in tools such as NTLite can copy the executable and profile and run the command above.
- **Scripted setup:** include a `choco install -y shutup10` step followed by the import command.
- **Premium in managed environments:** the Premium installer is an MSI. Its standard silent form is `msiexec.exe /i <installer>.msi /quiet /norestart`, run from an elevated prompt. Verify against current vendor documentation before large rollouts.

> One-time imports with the Free edition apply the settings once. They do not defend against later Windows changes.

## 12. Keeping Settings After Windows Updates

Windows feature updates and system changes can reset or re-enable options. There are two ways to deal with this.

**Free edition (manual):**
- Re-run the tool after major updates.
- Re-import your saved profile.
- Optionally schedule a script that imports your profile at logon or on a recurring task.

**Premium edition (automatic):**
- Continuously monitors your selected settings.
- Reapplies them when Windows changes them.
- Uses a client/service design, so end users do not need permanent admin rights.
- Can show notifications when settings are restored.

## 13. Trade-offs and What Can Break

Every privacy setting removes a feature or data flow. Be aware of the common ones:

| If you disable... | You may lose... |
|---|---|
| Location services | Weather, maps, "find my device", location-aware apps |
| Online speech recognition | Cloud-based dictation and voice features |
| Web search in Start | Bing suggestions (local results remain) |
| Cloud content in Start/widgets | Personalized recommendations and some widget content |
| Background apps | Notifications and background sync from some apps |
| Telemetry options | Some diagnostics and feedback features; certain restrictions may be limited on some Windows editions |
| OneDrive/account integration | Convenience of sync and sign-in features |
| Automatic hotspot connection | Convenience of auto-joining open networks (generally a security benefit) |

**Cautions:**

- Disabling **update-related** options can affect how and when your PC updates. Do not turn off anything that reduces security patching unless you understand the consequences.
- Settings sometimes behave differently on **Home vs. Pro vs. Enterprise** editions.
- Work or school devices may have policies that override or conflict with local changes.

## 14. Troubleshooting

| Problem | What to try |
|---|---|
| Something stopped working after applying settings | Identify the feature, find the matching setting by its description, and reset it individually |
| Many things broke | Use Undo, or restore the restore point you created |
| Settings reverted after an update | Re-apply or re-import your profile; consider Premium |
| Tool won't launch | Run as administrator; check whether security software is blocking the executable |
| Import does nothing | Confirm the path is correct and quoted; run from an elevated prompt |
| Settings don't apply on a managed PC | Organization policy may override local changes; check with your IT administrator |
| Option missing | Some settings only appear on specific Windows versions or builds |

## 15. Related: Manual Registry Method for Web Search

If you only want to turn off web results in Start menu search and do not want a third-party tool, the registry policy below does that on Windows 11:

```cmd
reg add "HKCU\Software\Policies\Microsoft\Windows\Explorer" /v DisableSearchBoxSuggestions /t REG_DWORD /d 1 /f
```

Then restart Explorer:

```cmd
taskkill /f /im explorer.exe & start explorer.exe
```

Use `HKLM` instead of `HKCU` to apply it for all users. Delete the value or set it to `0` to revert.

ShutUp10 includes a setting for disabling Bing and web search in Windows Search, along with many other options, so it is the better choice if you want to handle web search and other privacy settings together.

## 16. FAQ

**Is it really free?**
Yes. The vendor states the Free edition is and will remain free. Premium is optional and adds automation.

**Does it need to be installed?**
The Free edition does not. Premium is installed so it can run continuously.

**Is it safe to use?**
It changes real system settings, so use it carefully: create a restore point, start with recommended settings, and read descriptions before changing anything else.

**Will it stop all data collection?**
No tool can guarantee that. It reduces many data flows and features that Windows exposes as settings. Review your results and combine with other good practices.

**Do I need to run it after every Windows update?**
With the Free edition, it is wise to check after major updates. Premium handles this automatically.

**Can I use the same configuration on multiple PCs?**
Yes. Export a profile and import it on each machine, manually or via command line.

**Does it work on Windows 11?**
Yes. It supports both Windows 10 and Windows 11.

**Should I apply every setting?**
No. Start with the recommended ones and add others only when you understand the trade-off.

## 17. Resources

- Product overview: https://www.oo-software.com/en/shutup10
- Features: https://www.oo-software.com/en/shutup10/features
- Editions comparison: https://www.oo-software.com/en/shutup10/editions
- Premium: https://www.oo-software.com/en/shutup10/ooshutup10premium
- Screenshots: https://www.oo-software.com/en/shutup10/screenshots
- Support: https://www.oo-software.com/en/shutup10/support
- Changelog: https://www.oo-software.com/en/shutup10/changelog
- Online manuals: https://docs.oo-software.com/en/
- For further Windows hardening recommendations, the vendor points to guidance from the German Federal Office for Information Security (BSI).

---

*This guide is based on O&O Software's published product pages and community deployment examples. Features, pricing, and command-line options can change between versions, so check the official documentation for your installed version.*
