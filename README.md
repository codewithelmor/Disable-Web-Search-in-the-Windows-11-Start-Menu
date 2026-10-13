# Windows Setup, Privacy & Cleanup Guides

![Fuck MICROSLOP](https://c.tenor.com/dmUPx0eFh4AAAAAd/tenor.gif)


A collection of practical, step-by-step markdown guides for setting up, tightening, and cleaning a Windows 10/11 PC. Each guide is self-contained, written to be read top to bottom or used as a reference, and includes troubleshooting and a quick-reference section.

## What's Inside

| Guide | What it covers | Best for |
|---|---|---|
| [Disable Start Menu Web Search](Disable-Web-Search-Windows-11-Start-Menu.md) | Turning off Bing/web results in the Windows 11 Start menu using a registry policy (command line, Registry Editor, all-users option, revert) | A fast, tool-free privacy fix |
| [Windows 11 Local Account Install Guide](Windows-11-Local-Account-Install-Guide.md) | Installing Windows 11 without a Microsoft account using `start ms-cxh:localonly`, plus fallbacks (registry `BypassNRO`, Rufus media, `autounattend.xml`, switching accounts after setup) | Clean installs and fresh PCs |
| [O&O ShutUp10 Guide](OO-ShutUp10-Guide.md) | Using the free O&O ShutUp10 privacy tool: settings categories, recommended workflow, profile export/import, command-line deployment, Free vs. Premium | Hardening Windows privacy settings in one place |
| [Revo Uninstaller Guide](Revo-Uninstaller-Guide.md) | Removing programs and their leftovers with Revo Uninstaller Free and Pro: scan modes, Hunter Mode, Forced Uninstall, backups and recovery | Thorough software removal and cleanup |

## Suggested Order

If you are setting up a PC from scratch, the guides fit together as a workflow:

1. **Install:** [Windows 11 Local Account Install Guide](Windows-11-Local-Account-Install-Guide.md)
2. **Harden privacy:** [O&O ShutUp10 Guide](OO-ShutUp10-Guide.md), with [Disable Start Menu Web Search](Disable-Web-Search-Windows-11-Start-Menu.md) as a lightweight alternative or complement
3. **Clean up bloat:** [Revo Uninstaller Guide](Revo-Uninstaller-Guide.md)

## Common Themes

- **Privacy:** reducing telemetry, web search, ads, and account-linked data collection.
- **Control:** deciding what Windows installs, collects, and keeps.
- **Safety first:** every guide stresses restore points, backups, and reviewing changes before applying them.
- **Reversibility:** where possible, guides show how to undo each change.

## Before You Use Any Guide

- **Back up your data** and **create a System Restore Point** before changing system settings or removing software.
- **Use an administrator account.** Most steps involve system settings, the registry, or setup.
- **Read each step before running commands.** Some commands edit the registry or restart Explorer.
- **Test on a non-critical machine first** if you plan to deploy changes to several PCs.
- **Windows changes often.** Feature updates can reset settings, and installation tricks can stop working between builds.

## Accuracy and Currency

These guides were compiled from vendor documentation, community reports, and press coverage, with notes in each file where details were uncertain or build-dependent. In particular:

- The `start ms-cxh:localonly` install method is **build-dependent**, and Microsoft has said it is removing local-account bypasses.
- Software versions, pricing, and feature availability (O&O ShutUp10, Revo Uninstaller) change over time, so confirm on the vendors' sites.
- Each guide ends with a note describing its sources and caveats.

Last reviewed: October 2026.

## Repository Structure

```
.
├── README.md
├── Disable-Web-Search-Windows-11-Start-Menu.md
├── Windows-11-Local-Account-Install-Guide.md
├── OO-ShutUp10-Guide.md
└── Revo-Uninstaller-Guide.md
```

## Contributing and Maintaining

Suggestions for keeping the guides useful:

- **Re-verify time-sensitive claims** (Windows build behavior, versions, prices) when Windows or the tools release major updates.
- **Keep guides independent** so each can be read on its own, and link between them rather than duplicating content.
- **Note uncertainty** instead of presenting unverified steps as guaranteed.
- **Follow the existing layout:** overview, prerequisites, step-by-step instructions, troubleshooting, FAQ, quick reference.
- **Add new guides to the table above** and to the structure listing.

## Disclaimer

These guides are provided for informational purposes. Modifying system settings, the registry, or installation media carries risk, and results vary by Windows edition, build, and hardware. Follow the steps at your own discretion, keep backups, and respect the licenses and terms of any software and operating systems you use. This repository is not affiliated with Microsoft, O&O Software, or VS Revo Group.
