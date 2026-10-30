<div align="center">

# 🦁 Brave Origin

> **Turn Brave into Brave Origin — fully debloated, privacy-hardened, and actually fast.**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Platform](https://img.shields.io/badge/platform-Linux%20%7C%20macOS%20%7C%20Windows-blue)](#)
[![Stars](https://img.shields.io/github/stars/flyingPenguinW/brave-origin?style=flat&color=gold)](#)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen)](#)

### ☕ [Buy Me a Coffee](https://buymeacoffee.com/AilieIsQueen)

</div>

---

## ✨ What It Does

Brave is great, but it ships with a lot of extras most people never touch: **Rewards, Wallet, VPN, News, Talk, Tor, Playlist, Wayback Machine, Web Discovery and telemetry**. This project turns them off at the **system policy level**, meaning they don't just get hidden — they stop loading entirely. No background processes, no UI clutter, no wasted RAM.

It also covers features you may actually use (**Leo AI, Speedreader, sync, DevTools, autofill...**). That is why there are two levels, and you choose what stays:

- **Hard** (recommended) - removes the bloat and telemetry, keeps the useful features.
- **Extreme** - maximum lockdown, everything disabled.
- **Custom** - pick Hard / Extreme / Skip per category.

What each level does (the same table is shown by the scripts):

**Same in both:** Safe Browsing = Standard (Enhanced shares more visited links).

**Disabled in both levels**

| Setting | Extreme | Hard |
|---|---|---|
| Rewards / Wallet / VPN / News / Tor | off | off |
| Telemetry & tracking | off | off |
| Password manager | off | off |
| Search suggestions | off | off |
| Background mode | off | off |

**Differences**

| Setting | Extreme | Hard |
|---|---|---|
| Leo AI | off | **ON** |
| Speedreader | off | **ON** |
| Sync | off (all profiles) | **ON** |
| Add profile / guest mode | blocked | **allowed** |
| Address autofill | off | **ON** |
| Card autofill | off | Brave default |
| Translate & spellcheck | off | **ON** |
| Bookmarks bar | hidden | **shown** |
| New tab page | about:blank | **unchanged** |
| DevTools | off | **ON** |
| DNS-over-HTTPS | forced (AdGuard) | **your choice** (not locked) |
| Default search engine | Brave Search | **your choice** (not overridden) |

**Both levels also:** homepage = `about:blank`, Memory Saver ON, HTTPS upgrades ON. Shields (ad/tracker blocking) stay fully intact.

---

## 🚀 One-Click Setup

All three scripts (Linux, Windows, macOS) work the same way: they show a menu, offer a backup, and write the policies for the level you choose.

### 🐧 Linux

```bash
chmod +x setup.sh && ./setup.sh
```

### 🪟 Windows

- **Normal install:** Right-click `setup.bat` → **Run as Administrator**
- **Store install:** Run `setup.bat` as Admin — it will detect Store path and handle it

### 🍎 macOS

```bash
chmod +x setup_mac.sh && ./setup_mac.sh
```

### Debloat levels

The scripts show this menu:

1. **Hard** - same debloat, but keeps features you may actually use (recommended)
2. **Extreme** - maximum lockdown, everything disabled
3. **Custom** - choose Hard / Extreme / Skip per category
4. **Restore** - back to the original Brave state (from backup)

The comparison of what each level does is in the "What It Does" section at the top.

Policies lock the matching options in `brave://settings` ("managed by your organization"). Use **Restore** to undo.

### Backup & restore

Before changing anything the script offers to back up your current Brave policies (strongly recommended). An existing backup is never overwritten, so running the script again keeps your original state.

| Platform | Backup location | Restore |
|---|---|---|
| Linux | `~/.brave-origin-backup` (policy file + desktop entry) | `./setup.sh --restore` |
| Windows | `%USERPROFILE%\.brave-origin-backup` (registry export of the Brave policy key) | `setup.bat /restore` |
| macOS | `~/.brave-origin-backup` (managed plist + launcher app) | `./setup_mac.sh --restore` |

You can also run the script again and choose **4) Restore**. Without a backup, restore only removes the policy values created by the script (other policies are left alone).

Manual flags and settings in `brave://flags` / `brave://settings` are not touched by the scripts - revert them by hand if you changed them.

### 🤖 Android

See [Android note](#android).

**Verify:** Open `brave://policy` — the policies of the level you chose should be listed with status **OK** (see the [Policy Reference](#-policy-reference) for the values).

---

## 📋 Policy Reference

> Values written by each level. `—` = not set (Brave default, you can change it in the browser). The scripts generate these from the same list; `policies.json` / `brave-origin.reg` = Extreme, `policies-hard.json` / `brave-origin-hard.reg` = Hard.

### Brave bloat

| Policy | Extreme | Hard |
|--------|---------|------|
| `BraveRewardsDisabled` | `true` | `true` |
| `BraveWalletDisabled` | `true` | `true` |
| `BraveVPNDisabled` | `true` | `true` |
| `BraveNewsDisabled` | `true` | `true` |
| `BraveTalkDisabled` | `true` | `true` |
| `TorDisabled` | `true` | `true` |
| `BravePlaylistEnabled` | `false` | `false` |
| `BraveWaybackMachineEnabled` | `false` | `false` |

### Leo AI & Speedreader

| Policy | Extreme | Hard |
|--------|---------|------|
| `BraveAIChatEnabled` | `false` | — |
| `BraveSpeedreaderEnabled` | `false` | `true` |

### Telemetry & network

| Policy | Extreme | Hard |
|--------|---------|------|
| `BraveP3AEnabled` | `false` | `false` |
| `BraveStatsPingEnabled` | `false` | `false` |
| `BraveWebDiscoveryEnabled` | `false` | `false` |
| `MetricsReportingEnabled` | `false` | `false` |
| `UserFeedbackAllowed` | `false` | `false` |
| `PrivacySandboxAdTopicsEnabled` | `false` | `false` |
| `PrivacySandboxPromptEnabled` | `false` | `false` |
| `PrivacySandboxSiteEnabledAdsEnabled` | `false` | `false` |
| `PaymentMethodQueryEnabled` | `false` | `false` |
| `AlternateErrorPagesEnabled` | `false` | `false` |
| `NetworkPredictionOptions` | `0` | `0` |
| `SearchSuggestEnabled` | `false` | `false` |

### Privacy (DNS, Safe Browsing)

| Policy | Extreme | Hard |
|--------|---------|------|
| `SafeBrowsingProtectionLevel` | `1` | `1` |
| `DnsOverHttpsMode` | `secure` | — |
| `DnsOverHttpsTemplates` | `https://dns.adguard-dns.com/dns-query` | — |

### Sync & profiles

| Policy | Extreme | Hard |
|--------|---------|------|
| `SyncDisabled` | `true` | — |
| `BrowserAddPersonEnabled` | `false` | — |
| `BrowserGuestModeEnabled` | `false` | — |

### Passwords, autofill, translate & spellcheck

| Policy | Extreme | Hard |
|--------|---------|------|
| `PasswordManagerEnabled` | `false` | `false` |
| `AutofillAddressEnabled` | `false` | `true` |
| `AutofillCreditCardEnabled` | `false` | — |
| `TranslateEnabled` | `false` | `true` |
| `SpellcheckEnabled` | `false` | `true` |
| `SpellcheckServiceEnabled` | `false` | `false` |

### UI tweaks

| Policy | Extreme | Hard |
|--------|---------|------|
| `ShowHomeButton` | `false` | `false` |
| `HomepageLocation` | `about:blank` | `about:blank` |
| `DefaultBrowserSettingEnabled` | `false` | `false` |
| `BookmarkBarEnabled` | `false` | `true` |
| `NewTabPageLocation` | `about:blank` | — |

### Developer tools

| Policy | Extreme | Hard |
|--------|---------|------|
| `DeveloperToolsAvailability` | `2` | `1` |

### Search engine

| Policy | Extreme | Hard |
|--------|---------|------|
| `DefaultSearchProviderEnabled` | `true` | — |
| `DefaultSearchProviderName` | `Brave Search` | — |
| `DefaultSearchProviderSearchURL` | `https://search.brave.com/search?q={searchTerms}` | — |
| `ManagedSearchEngines` | Brave Search, Google, DuckDuckGo | — |

### Performance & misc

| Policy | Extreme | Hard |
|--------|---------|------|
| `BackgroundModeEnabled` | `false` | `false` |
| `HighEfficiencyModeEnabled` | `true` | `true` |
| `ComponentUpdatesEnabled` | `true` | `true` |
| `HttpsUpgradesEnabled` | `true` | `true` |
| `IncognitoModeAvailability` | `0` | `0` |
| `DownloadRestrictions` | `0` | `0` |
| `PromptForDownloadLocation` | `true` | `true` |
| `PrintingEnabled` | `true` | `true` |

`NetworkPredictionOptions = 0` keeps DNS prefetch and preconnect enabled (speed fix) in both levels.

---

## ⚡ Speed Fix

Pages loading slow? `NetworkPredictionOptions` is set to **0** (full prediction) — this re-enables:

- ✅ DNS prefetching
- ✅ TCP/SSL preconnection
- ✅ Prerendering

If still slow, your secure DNS provider might be the bottleneck:

- **Hard:** DNS is not locked. Change it in Brave settings (search for "secure DNS"; usually `brave://settings/security`).
- **Extreme:** the provider is forced by policy (AdGuard) and cannot be changed in settings. Edit `DnsOverHttpsTemplates` in `setup.sh` / `setup.bat` / `setup_mac.sh` and run it again.

| Provider | Template |
|----------|----------|
| **AdGuard** (default in Extreme) | `https://dns.adguard-dns.com/dns-query` |
| **Cloudflare** (fast) | `https://cloudflare-dns.com/dns-query` |
| **Quad9** (secure) | `https://dns.quad9.net/dns-query` |

---

## 🧩 Post-Setup (Do These Once)

```
brave://flags/#brave-sidebar            → Disabled
brave://flags/#enable-zero-copy          → Enabled
brave://flags/#enable-parallel-downloading → Enabled
brave://settings/appearance              → "Use system title bar and borders" ON
brave://settings/system                  → "Memory Saver" ON
brave://settings/security                → "Use secure DNS" → choose a provider (Hard only)
```

> **DoH (DNS-over-HTTPS)** encrypts the website lookups your browser makes, so your ISP and the local network can't see which sites you visit. It does not hide your IP and does not block ads.

---

## 🎨 Replacing the Brave Logo

The setup scripts do **not** touch the Brave icon. If you want to use a custom logo, do it manually per platform:

### Linux
```bash
# Replace the system Brave icon (256x256 is the app menu size)
sudo cp /path/to/your-logo.svg /usr/share/icons/hicolor/scalable/apps/brave-browser.svg
# Or for PNG:
# sudo cp /path/to/your-logo.png /usr/share/icons/hicolor/256x256/apps/brave-browser.png
sudo gtk-update-icon-cache /usr/share/icons/hicolor/
```

### macOS
Replace the app icon in the `.app` bundle:
```bash
# Convert your .png to .icns first
sudo cp /path/to/your-logo.icns /Applications/Brave\ Browser.app/Contents/Resources/app.icns
# Clear icon cache
sudo rm -rf /Library/Caches/com.apple.iconservices.store
```

### Windows
Create a desktop shortcut and point its icon to your `.ico` file:
1. Convert your logo to `.ico` (e.g. [convertio.co](https://convertio.co/png-ico/))
2. Right-click the Brave shortcut → **Properties** → **Change Icon** → browse to your `.ico`
3. For Store installs, create a shortcut from `%LOCALAPPDATA%\BraveSoftware\Brave-Browser\Application\brave.exe`

---

## 📂 File Reference

| File | Platform | Purpose |
|------|----------|---------|
| `policies.json` | All | Complete policy definitions (Extreme) |
| `policies-hard.json` | All | Complete policy definitions (Hard) |
| `setup.sh` | Linux | Menu, backup/restore, policy deploy + desktop entry patch |
| `setup.bat` | Windows | Menu, backup/restore, registry policies + shortcut flags (normal & Store) |
| `setup_mac.sh` | macOS | Menu, backup/restore, plist deployment + launcher app with flags |
| `brave-origin.reg` | Windows | Manual registry import (Extreme) |
| `brave-origin-hard.reg` | Windows | Manual registry import (Hard) |

---

## 🤖 Android

Android Brave **does not support enterprise policies**. However:

1. `brave://flags/#brave-sidebar` → **Disabled**
2. `brave://flags/#enable-parallel-downloading` → **Enabled**
3. Settings → Rewards / Wallet / Leo → disable individually

Root users: add `--disable-features=AIChat,BraveVPN` via `brave_app_flags`.

---

<div align="center">

### ☕ [Buy Me a Coffee](https://buymeacoffee.com/AilieIsQueen)

**Your support keeps this project maintained and improving!**

---

**Brave Origin** — *Privacy without the bloat.*

</div>
