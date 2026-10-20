# Proxya Desktop 1.0.0

First release of Proxya Desktop, a SOCKS5 and HTTP proxy client for Windows and
macOS with a TUN tunnel, app routing and residential proxy generation.

## Install

### Windows x64

- `Proxya_1.0.0_x64-setup.exe` — installer.

Builds are not Authenticode signed yet. SmartScreen can show an unknown
publisher, so verify the SHA-256 before choosing **Run anyway**. See
[Install on Windows](https://github.com/ProxyaAnty/Proxya-Desktop/blob/main/docs/windows-installation.md).

### macOS Apple Silicon

- `Proxya-macos-arm64.tar.gz` — the application bundle.

Ad-hoc signed and not notarized. See
[Install on macOS](https://github.com/ProxyaAnty/Proxya-Desktop/blob/main/docs/mac-installation.md) for the one-time Gatekeeper step,
and the same guide [in Russian](https://github.com/ProxyaAnty/Proxya-Desktop/blob/main/docs/mac-установка.md). Intel Macs are not
supported.

### Verify your download

Compare the download's SHA-256 with `SHA256SUMS.txt` attached to this release.

Windows PowerShell:

```powershell
Get-FileHash .\Proxya_1.0.0_x64-setup.exe -Algorithm SHA256
```

macOS Terminal:

```bash
shasum -a 256 Proxya-macos-arm64.tar.gz
```

## What is in it

- A whole-machine tunnel through a TUN adapter, carrying TCP and UDP, with DNS
  intercepted and QUIC working when the proxy relays UDP.
- System proxy mode, which needs no service and no administrator rights.
- Routing by program and by site. All programs, all except the ones you pick, or
  only the ones you pick. Sites and addresses direct, local network direct,
  Russian sites direct.
- **Masking.** The handshake to the proxy leaves in pieces, so a provider that
  reads the destination address out of a single packet finds nothing to match.
  Measured against one Russian provider and the Telegram data centres over the
  same proxy and the same link: one connection in six completed with the
  handshake in a single packet, six in six with it split. It is not encryption
  and is not sold as one, and the README says exactly what it does and does not
  hide.
- Kill switch on Windows.
- Proxy probing before every connection, covering login, the UDP relay and the
  country the exit reports.
- Generate residential SOCKS5 proxies directly in the app using your Proxya
  traffic balance: choose a country, a sticky IP or rotation, and UDP support,
  then connect immediately or save the proxy for later. Account sign-in also
  brings your datacenter, ISP and mobile orders into the app.
- English, Russian and Chinese, switched without a restart.

## Known limits

- The kill switch is Windows only. It is hidden on macOS rather than shown as a
  switch that does nothing.
- A VPN that manages DNS itself keeps its resolver in front of ours. Use system
  proxy mode beside one.
- IPv6 is off by default, because a proxy without IPv6 of its own accepts an
  IPv6 connection and then drops it.
- The Windows installer is not Authenticode signed. The macOS app is ad-hoc
  signed and is not notarized.
