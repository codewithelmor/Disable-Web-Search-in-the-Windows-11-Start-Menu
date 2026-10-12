# Installing Windows 11 with a Local Account (`start ms-cxh:localonly`)

A step-by-step guide to installing Windows 11 without signing in to a Microsoft account, using the `start ms-cxh:localonly` command during setup (OOBE), plus fallbacks for when it doesn't work.

> **Read this first: this method is build-dependent.**
> Microsoft has said it is removing known local-account bypasses from setup, and reports conflict. Some people still see it work on certain 25H2 retail media, others find it blocked on newer builds. Treat `start ms-cxh:localonly` as "try first," not "guaranteed." Section 7 covers reliable alternatives.
> *Status checked October 13, 2026. Re-verify against your specific ISO/build.*

---

## Table of Contents

1. [Overview](#1-overview)
2. [Will It Work on My System?](#2-will-it-work-on-my-system)
3. [Prerequisites](#3-prerequisites)
4. [Create the Installation Media](#4-create-the-installation-media)
5. [Install Windows 11](#5-install-windows-11)
6. [The `start ms-cxh:localonly` Method (Step by Step)](#6-the-start-ms-cxhlocalonly-method-step-by-step)
7. [If It Doesn't Work: Alternatives](#7-if-it-doesnt-work-alternatives)
8. [First Boot Checklist](#8-first-boot-checklist)
9. [Privacy Hardening After Install](#9-privacy-hardening-after-install)
10. [Troubleshooting](#10-troubleshooting)
11. [Trade-offs of a Local Account](#11-trade-offs-of-a-local-account)
12. [FAQ](#12-faq)
13. [Quick Reference](#13-quick-reference)

---

## 1. Overview

During Windows 11's Out-of-Box Experience (OOBE), setup pushes you to connect to the internet and sign in with a Microsoft account. `ms-cxh:localonly` is a URI that launches the "Create a user for this PC" dialog, letting you make a local (offline) account instead.

The command is typed into a Command Prompt opened during setup with **Shift + F10**.

```cmd
start ms-cxh:localonly
```

**Spelling matters.** It is `ms-cxh` (not `ms-chx`). The documented form has no `//`. Variants you may see in forums:

| Variant | Notes |
|---|---|
| `start ms-cxh:localonly` | The standard form. Try this first. |
| `start ms-cxh://setaddlocalonly` | Reported to open the Windows 11-style dialog rather than the older Windows 8/10-style view. |
| `WinJS.Application.restart("ms-cxh://LOCALONLY")` | Entered in the developer console (Ctrl + Shift + J) on the sign-in screen instead of Command Prompt. |

## 2. Will It Work on My System?

There is no single answer. What reports indicate:

| Factor | Effect |
|---|---|
| **Windows build** | Behavior differs between 24H2, 25H2, and newer builds. Microsoft has publicly said it is removing known local-account mechanisms, including this command. |
| **Edition** | Reports suggest Pro is more forgiving than Home. Home officially requires a Microsoft account to finish setup. |
| **Install media** | Some retail 25H2 media reportedly still respond; newer images and cumulative OOBE updates may block it. |
| **Timing** | The command only works at the right screen (see Section 6). Running it too late is a common failure. |
| **Managed/organization flow** | If OOBE redirects to a work or school flow, the dialog may not appear. |

**Practical advice:** try the command; if the dialog doesn't open within a couple of attempts, move to Section 7 rather than looping.

## 3. Prerequisites

- **A PC that meets Windows 11 requirements** (this guide does not cover bypassing hardware checks).
- **A USB drive of at least 8 GB** (it will be erased).
- **A second PC** with internet access to prepare the media.
- **Backups.** A clean install wipes the target drive/partition.
- **Product key or digital license** (many PCs activate automatically after install).
- **Drivers**, especially network and storage drivers, if your hardware needs them.
- **The edition you intend to install** (Home or Pro). Pro generally gives you more options.

## 4. Create the Installation Media

### Option A: Microsoft's Media Creation Tool (official)

1. Download Windows 11 media from Microsoft's official download page.
2. Run the Media Creation Tool and choose **USB flash drive**.
3. Let it download and write the installer.

### Option B: Download the ISO and use Rufus (recommended if you want fewer setup prompts)

1. Download the official Windows 11 ISO from Microsoft.
2. Download Rufus from its official site.
3. Select the ISO, choose your target device, and click **Start**.
4. Rufus can offer customization options when writing Windows 11 media. These can include creating a local account and skipping the online-account requirement. If you use these, you may not need Section 6 at all.

> Always download from official sources. Verify the ISO against Microsoft's published hash if you want extra assurance.

## 5. Install Windows 11

1. **Boot from the USB.** Open the boot menu (commonly F12, F10, F8, Esc, or Del depending on the manufacturer) and select the USB device.
2. **Choose language, time format, and keyboard**, then click **Next → Install now**.
3. **Enter a product key** or select **I don't have a product key** if your hardware has a digital license.
4. **Select the edition** if prompted.
5. **Accept the license terms.**
6. **Choose Custom: Install Windows only.**
7. **Select the drive or partition** and install. (Delete partitions only if you intend a full wipe.)
8. **Wait for files to copy.** The PC restarts one or more times. **Remove the USB when it first reboots into OOBE** if it tries to boot setup again.

After the reboots, you arrive at OOBE: region selection, keyboard layout, and then network/account screens. This is where the next section begins.

## 6. The `start ms-cxh:localonly` Method (Step by Step)

### Step 1: Reach OOBE

Continue past the initial region selection.

### Step 2: Get the timing right

This is the most common point of failure. Reports describe two working points:

- **At the Microsoft account sign-in screen**, or
- **Immediately after you choose the keyboard layout**, early in OOBE.

One user report found the command only worked right after selecting the keyboard layout and failed when run later in OOBE. If you are past that point, see "Reset OOBE" below.

### Step 3: Open Command Prompt

Press **Shift + F10**. On laptops you may need **Shift + Fn + F10**.

A black Command Prompt window opens on top of setup. If nothing appears, click the setup window once and try again.

### Step 4: Run the command

Type exactly:

```cmd
start ms-cxh:localonly
```

Press **Enter**.

### Step 5: Create the local account

If it works, a dialog appears asking you to create a user for this PC.

1. Enter a **user name**.
2. Enter a **password** (or leave blank; see Section 11 for the risks).
3. If asked, add **security questions**.
4. Confirm.

Setup then continues through the remaining screens (privacy options, etc.) and boots to the desktop with a local account.

### Step 6: If the dialog doesn't appear

- Confirm the spelling, with no extra characters or `//`.
- Retype it at a different OOBE screen, preferably the sign-in screen.
- Try the Windows 11-style variant: `start ms-cxh://setaddlocalonly`.
- Try the developer-console version (Ctrl + Shift + J, then the `WinJS.Application.restart("ms-cxh://LOCALONLY")` line) on the sign-in screen.
- Go to **Reset OOBE** below, then retry at the keyboard-layout screen.
- If it still fails, the build probably blocks it. Go to Section 7.

### Reset OOBE (to retry the timing)

If you've gone past the right point:

1. Press **Shift + F10**.
2. Open Task Manager by typing `taskmgr` in the prompt.
3. End the Microsoft account setup process or app.
4. Setup should return to an earlier screen (the language/keyboard step), giving you another chance to run the command at the correct moment.

Behavior varies by build; a restart of the installation may be simpler.

## 7. If It Doesn't Work: Alternatives

Listed roughly from least to most effort.

### 7.1 Registry `BypassNRO`, then disconnect the network

On some media, this still works as a fallback. At OOBE:

1. Press **Shift + F10**.
2. Run:
   ```cmd
   reg add HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\OOBE /v BypassNRO /t REG_DWORD /d 1 /f
   shutdown /r /t 0
   ```
3. After the restart, choose **I don't have internet** (or disconnect the network) when prompted, then **Continue with limited setup**.

The older `OOBE\BYPASSNRO` script is build-dependent and has been removed from newer builds. The registry variant is the one worth trying.

### 7.2 Disconnect from the network

- **Don't connect Wi-Fi** at the network screen, and unplug Ethernet before OOBE.
- On some builds, a failed network check offers a local-account path.
- This is unreliable on current builds but costs nothing to try.

### 7.3 Use Rufus-customized media

Rufus can write Windows 11 media that skips the online-account requirement and creates a local account for you. This is one of the most dependable options because it changes the media rather than relying on an OOBE command. It requires a clean install.

### 7.4 Unattended install with an answer file

For repeatable or deployment scenarios, provide an `autounattend.xml` that defines a local account and hides the online-account screens. This is the supported mechanism for automating setup.

A trimmed, **illustrative** example of the relevant `oobeSystem` section:

```xml
<component name="Microsoft-Windows-Shell-Setup" processorArchitecture="amd64"
           publicKeyToken="31bf3856ad364e35" language="neutral" versionScope="nonSxS"
           xmlns:wcm="http://schemas.microsoft.com/WMIConfig/2002/State">
  <OOBE>
    <HideEULAPage>true</HideEULAPage>
    <HideOnlineAccountScreens>true</HideOnlineAccountScreens>
    <HideWirelessSetupInOOBE>true</HideWirelessSetupInOOBE>
    <ProtectYourPC>3</ProtectYourPC>
  </OOBE>
  <UserAccounts>
    <LocalAccounts>
      <LocalAccount wcm:action="add">
        <Name>YourUserName</Name>
        <Group>Administrators</Group>
        <Password>
          <Value>ChangeMe</Value>
          <PlainText>true</PlainText>
        </Password>
      </LocalAccount>
    </LocalAccounts>
  </UserAccounts>
</component>
```

Place the file named `autounattend.xml` at the root of the USB drive. Build and validate it with Microsoft's tooling (Windows System Image Manager) before relying on it. Don't store real passwords in plain text beyond initial setup; change them after first login.

### 7.5 Finish with a Microsoft account, then switch (most reliable)

If nothing else works, this always works, at the cost of briefly using an online account:

1. Complete setup signed in with a Microsoft account (a throwaway one is fine).
2. Go to **Settings → Accounts → Other users → Add account**, and create a local user.
3. Set that user's type to **Administrator**.
4. Sign out and sign in as the local user.
5. Remove the Microsoft account from **Settings → Accounts → Other users**.

Windows may still sync some data while the Microsoft account is present, so remove it promptly.

### 7.6 Pro-only: domain or work/school path

On Pro, the "Set up for work or school" route with domain join can avoid the personal-account requirement. This is intended for organizations, so use it only if it fits your situation.

### Comparison

| Method | Reliability on current builds | Effort | Keeps a clean install |
|---|---|---|---|
| `start ms-cxh:localonly` | Varies by build | Very low | Yes |
| Registry `BypassNRO` | Build-dependent | Low | Yes |
| Network disconnect | Low | Very low | Yes |
| Rufus-customized media | High | Low-medium | Yes |
| `autounattend.xml` | High | Medium-high | Yes |
| MSA first, then switch | Very high | Low | Yes (brief online account) |

## 8. First Boot Checklist

After reaching the desktop:

1. **Run Windows Update** and install pending updates and drivers.
2. **Confirm activation** in **Settings → System → Activation**.
3. **Check your account type** in **Settings → Accounts → Your info** (it should show a local account).
4. **Set a password and recovery options.** Local accounts have no online reset, so record your password safely. Configure security questions or a recovery method.
5. **Create a second administrator** or password reset disk as a safety net.
6. **Review privacy settings** (Section 9).
7. **Create a restore point** once your baseline is configured.
8. **Consider enabling disk encryption** where available. Note that BitLocker/Device Encryption recovery keys are normally backed up to a Microsoft account, so with a local account you must save the recovery key yourself.

## 9. Privacy Hardening After Install

A local account removes the account link, but Windows still has telemetry, suggestions, and web search enabled by default.

- **Disable web results in Start search** with the registry policy:
  ```cmd
  reg add "HKCU\Software\Policies\Microsoft\Windows\Explorer" /v DisableSearchBoxSuggestions /t REG_DWORD /d 1 /f
  taskkill /f /im explorer.exe & start explorer.exe
  ```
- **Use O&O ShutUp10** to manage around 300 privacy and system settings in one place, apply recommended settings, and export a profile for reuse. See the companion guide, `OO-ShutUp10-Guide.md`.
- **Review Settings → Privacy & security** for app permissions, diagnostics, and advertising ID.
- **Re-check after major Windows updates**, since updates can reset settings.

## 10. Troubleshooting

| Problem | Likely cause | What to try |
|---|---|---|
| Shift + F10 does nothing | Focus is on setup window; keyboard needs Fn | Click the setup window; try Shift + Fn + F10 |
| "Not recognized" / no dialog after command | Build blocks it, or wrong screen | Retype at the sign-in screen; check spelling; see Section 7 |
| Dialog opens then setup loops | OOBE redirect or incomplete state | Reset OOBE via Task Manager; or restart install and retry earlier |
| Setup insists on internet | Network requirement still enforced | Registry `BypassNRO` + reboot; or Rufus media |
| Forced into work/school sign-in | Managed or redirected flow | Use Rufus media, an answer file, or Section 7.5 |
| Local account created but can't sign in later | Password typo or no recovery set | Use a second admin account, or reset via recovery options |
| Windows Home blocks everything | Home officially requires an MSA | Use Section 7.3, 7.4, or 7.5; consider Pro |
| Skipped setup screens leave device half-configured | Bypass skips some OOBE steps | Revisit **Settings** for privacy, region, and update options |
| BitLocker/Device Encryption asks for a key you don't have | Key wasn't backed up | Prevent this by saving the key during setup; if already locked, recovery may be impossible |

## 11. Trade-offs of a Local Account

**Benefits**
- No Microsoft account required to use the PC.
- Less account-linked syncing and fewer cloud prompts.
- Works well for offline, kiosk, lab, and privacy-focused machines.

**Costs**
- **No password reset via Microsoft account.** Lose the password, and recovery is harder.
- **Encryption recovery keys** won't be backed up automatically.
- **Some features expect a Microsoft account:** Microsoft Store purchases sync, OneDrive, cross-device sync, "Find my device," and some apps.
- **A blank password** is convenient but leaves the account weakly protected and can limit some network and remote features. Prefer a real password or PIN.
- **Microsoft's stated position** is that these bypasses can skip important setup screens and leave a device not fully configured. Check settings after install.

## 12. FAQ

**Does `start ms-cxh:localonly` still work?**
Sometimes. Reports differ by build and media, and Microsoft has said it is removing such mechanisms. Test on your image; don't build a process around it.

**Why does the spelling matter so much?**
Because the URI scheme is `ms-cxh`. Typos like `ms-chx` do nothing.

**Do I need to be offline?**
Not necessarily for this command; some reports say it works with the internet connected. Disconnecting is a separate fallback.

**Home or Pro?**
Pro tends to offer more flexibility. Home officially requires a Microsoft account to finish setup, so Home users should expect to rely on Rufus media, an answer file, or switching afterward.

**Is this safe?**
It's a documented-by-the-community setup shortcut, not malware. The risk is mainly a less-configured device and weaker recovery options, which the checklist above addresses.

**Can I do this on an already-installed PC?**
Yes: create a local admin account in Settings and remove the Microsoft account (Section 7.5), without reinstalling.

**Will Windows Update or activation break?**
No. Updates and activation work normally with a local account.

**Does a local account stop telemetry?**
No. It removes the account link but not Windows data collection. Use the privacy steps in Section 9.

## 13. Quick Reference

```
At OOBE:
  Shift + F10  →  start ms-cxh:localonly  →  create user

If no dialog:
  start ms-cxh://setaddlocalonly
  Retry right after the keyboard layout screen (Reset OOBE via taskmgr if needed)

Fallbacks:
  reg add HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\OOBE /v BypassNRO /t REG_DWORD /d 1 /f
  shutdown /r /t 0

Most reliable:
  Rufus-customized media  |  autounattend.xml  |  MSA first, then switch to local

After install:
  Windows Update → set password/recovery → save BitLocker key → privacy hardening
```

---

*Compiled from community reports, third-party guides, and press coverage of Microsoft's setup changes as of October 2026. Methods and behavior change frequently between Windows builds, so confirm against your installation media before relying on any step.*
