# Changelog

## 1.0.0

First public release.

- Whole-machine tunnel through a TUN adapter, for TCP and UDP, with DNS
  intercepted and QUIC carried when the proxy relays UDP.
- System proxy mode for machines where a service is not wanted or another VPN
  is already running.
- Routing by program and by site, with the local network and Russian sites able
  to stay direct.
- Masking, which sends the handshake to the proxy in pieces so that a provider
  reading the destination address out of a single packet finds nothing. This is
  what makes Telegram work on networks where a plain proxy connection dies.
- Kill switch on Windows, built on the Windows Filtering Platform. While it is
  armed nothing leaves the machine outside the adapter.
- Proxy probing before every connection, covering login, the UDP relay and the
  country of the exit.
- Proxya account sign-in with a password or with Google, bringing datacenter,
  ISP and mobile orders into the app and generating residential proxies against
  a GB balance.
- English, Russian and Chinese, switched without a restart.
- On macOS the service takes over the system DNS while the tunnel is up and
  restores the previous servers afterwards, with a copy on disk so a crash
  cannot leave the machine without a resolver.
