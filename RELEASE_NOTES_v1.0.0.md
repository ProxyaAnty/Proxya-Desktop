# Proxya Desktop 1.0.0

Proxya Desktop is a SOCKS5 and HTTP proxy client for Windows and macOS with
TUN tunneling, split tunneling and residential proxy generation.

## Features

- TUN tunnel for TCP traffic and UDP/QUIC when supported by the SOCKS5 proxy.
- System proxy mode for compatible applications.
- Routing rules for applications, websites, IP addresses and the local network.
- Residential SOCKS5 proxy generation from your Proxya traffic balance, with
  country selection, a sticky IP or rotation, and optional UDP support.
- Access to active datacenter, ISP and mobile proxy orders in your account.
- Proxy authentication and UDP availability checks before connecting.
- DNS over HTTPS and optional proxy handshake masking.
- Windows kill switch.
- English, Russian and Chinese interface languages.

## Downloads

| Platform | Asset | Installation guide |
| --- | --- | --- |
| Windows x64 | `Proxya_1.0.0_x64-setup.exe` | [Windows guide](https://github.com/ProxyaAnty/Proxya-Desktop/blob/main/docs/windows-installation.md) |
| macOS Apple Silicon | `Proxya-macos-arm64.tar.gz` | [macOS guide](https://github.com/ProxyaAnty/Proxya-Desktop/blob/main/docs/mac-installation.md), [Russian guide](https://github.com/ProxyaAnty/Proxya-Desktop/blob/main/docs/mac-%D1%83%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0.md) |

The Windows installer is not Authenticode signed. The macOS app is ad-hoc
signed and is not notarized. Follow the relevant installation guide if the
operating system blocks the download.

## Verify your download

Compare the download's SHA-256 with `SHA256SUMS.txt` attached to this release.

Windows PowerShell:

```powershell
Get-FileHash .\Proxya_1.0.0_x64-setup.exe -Algorithm SHA256
```

macOS Terminal:

```bash
shasum -a 256 Proxya-macos-arm64.tar.gz
```

## Platform limitations

- The kill switch is available on Windows only.
- The macOS build supports Apple Silicon; Intel Macs are not supported.
- IPv6 is disabled by default and requires a proxy with IPv6 support.
- Another VPN may conflict with tunnel routing or DNS. Use system proxy mode
  with compatible applications when running alongside a VPN.
