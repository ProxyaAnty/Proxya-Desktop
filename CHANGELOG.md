# Changelog

## 1.1.0

- Masking now also splits the site name inside the stream (the TLS server name,
  or the HTTP `Host` header), and splits the proxy handshake at a random point
  inside the address with a random 10–30 ms pause.
- The proxy handshake is sent in one go: connections through a masked proxy
  open about 0.4 s faster. Proxies that need the step-by-step exchange are
  detected automatically.
- System proxy mode works beside another VPN: direct connections resolve names
  through the system resolver instead of timing out.
- On Windows, tunnel mode checks whether another VPN takes the traffic and, if
  so, disconnects with an explanation and releases the kill switch.
- Removed the "Russian sites direct" routing option.
- "No DNS" is renamed "Resolved by the proxy" and remains the default.
- Notifications, error messages, the tray menu and the Google sign-in page
  follow the interface language.
- The app list refreshes while it is open, so newly started apps appear on
  their own.
- The proxy actions menu is no longer clipped by the proxy list. Radio buttons
  and short error messages are centred.
- Build machine paths are no longer embedded in the binaries.
- macOS: a disk image (`.dmg`) is published alongside the archive.

## 1.0.0

Initial public release of Proxya Desktop for Windows x64 and macOS Apple Silicon.

- Added TUN tunneling for TCP and supported UDP/QUIC traffic.
- Added system proxy mode for compatible applications.
- Added split tunneling by application, website, IP address and local network.
- Added residential SOCKS5 proxy generation with country selection, a sticky
  IP or rotation, and optional UDP support.
- Added Proxya account sign-in by password or Google, with access to active
  datacenter, ISP and mobile orders and the residential traffic balance.
- Added proxy authentication, UDP relay and exit location checks.
- Added DNS over HTTPS and optional proxy handshake masking.
- Added a Windows kill switch using Windows Filtering Platform.
- Added DNS configuration and restoration for tunnel mode on macOS.
- Added English, Russian and Chinese interface languages.
