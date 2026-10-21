# Proxya Desktop 1.1.0

## What's new

- **Stronger masking.** Besides the address in the proxy handshake, masking now
  splits the site name inside the stream (TLS server name or HTTP `Host`), at a
  random point and with a random pause. On a network that filters individual
  packets, Telegram and Instagram through the same proxies went from 0 of 25 to
  36 of 36 connections.
- **Faster connections.** The proxy handshake is sent in one go, about 0.4 s
  faster per connection with masking on.
- **Beside another VPN.** System proxy mode no longer stalls direct connections
  next to another VPN. On Windows, tunnel mode detects another VPN taking the
  traffic and disconnects with an explanation instead of showing a connection
  that is not in effect.
- **Languages.** Notifications, error messages, the tray menu and the Google
  sign-in page follow the interface language.
- **Interface.** The app list refreshes while open, the proxy actions menu is no
  longer clipped, radio buttons and short errors are centred.
- Removed the "Russian sites direct" routing option. "No DNS" is renamed
  "Resolved by the proxy" and remains the default.
- macOS: a `.dmg` is published alongside the `.tar.gz`.

## Downloads

| Platform | Download | Installation guide |
| --- | --- | --- |
| Windows x64 | [![Download the Windows installer](https://img.shields.io/badge/Download-Windows%20installer-0078D4?style=for-the-badge)](https://github.com/ProxyaAnty/Proxya-Desktop/releases/download/v1.1.0/Proxya_1.1.0_x64-setup.exe)<br><sub>`Proxya_1.1.0_x64-setup.exe`</sub> | [Windows guide](https://github.com/ProxyaAnty/Proxya-Desktop/blob/main/docs/windows-installation.md) |
| macOS Apple Silicon | [![Download the macOS disk image](https://img.shields.io/badge/Download-macOS%20.dmg-1d1d1f?style=for-the-badge&logo=apple&logoColor=white)](https://github.com/ProxyaAnty/Proxya-Desktop/releases/download/v1.1.0/Proxya-macos-arm64.dmg)<br><sub>`Proxya-macos-arm64.dmg`, or the [`.tar.gz` archive](https://github.com/ProxyaAnty/Proxya-Desktop/releases/download/v1.1.0/Proxya-macos-arm64.tar.gz)</sub> | [macOS guide](https://github.com/ProxyaAnty/Proxya-Desktop/blob/main/docs/mac-installation.md), [Russian guide](https://github.com/ProxyaAnty/Proxya-Desktop/blob/main/docs/mac-%D1%83%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0.md) |

The Windows installer is not Authenticode signed. The macOS app is ad-hoc
signed and is not notarized. Follow the relevant installation guide if the
operating system blocks the download. Installing over 1.0.0 keeps your proxies
and settings.

## Verify your download

Compare the download's SHA-256 with `SHA256SUMS.txt` attached to this release.

Windows PowerShell:

```powershell
Get-FileHash .\Proxya_1.1.0_x64-setup.exe -Algorithm SHA256
```

macOS Terminal:

```bash
shasum -a 256 Proxya-macos-arm64.dmg
```

## Platform limitations

- The kill switch is available on Windows only.
- The macOS build supports Apple Silicon. Intel Macs are not supported.
- IPv6 is disabled by default and requires a proxy with IPv6 support.
- Beside another VPN, use system proxy mode.
