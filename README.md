# Proxya Desktop

<p align="center">
  <img src="public/icon.png" width="112" height="112" alt="Proxya Desktop logo">
</p>

<p align="center">
  <strong><a href="https://github.com/ProxyaAnty/Proxya-Desktop/releases/latest">Download Proxya Desktop</a></strong><br>
  Windows x64, macOS Apple Silicon
</p>

**SOCKS5 and HTTP proxy client for Windows and macOS, by
[Proxya](https://proxya.co). Route your computer's traffic through a TUN tunnel,
choose which apps and sites use the proxy, and generate residential proxies
directly in the desktop app.**

[![License: MIT docs](https://img.shields.io/badge/docs%20license-MIT-2ea44f)](LICENSE)
[![Platforms](https://img.shields.io/badge/platforms-Windows%20x64%20%7C%20macOS%20arm64-444)](https://github.com/ProxyaAnty/Proxya-Desktop/releases/latest)

Point it at any SOCKS5 or HTTP proxy, or sign in and pull the ones you already
own from your Proxya account. The engine is sing-box, driven by a privileged
service that builds its own configuration from vetted fields, so nothing a
regular process can write ever reaches it.

> This repository holds the documentation, issue tracker and release downloads.
> The desktop application itself is proprietary and is distributed only as a
> release binary. See [BINARY-LICENSE.md](BINARY-LICENSE.md).

## What it does

- **Whole-machine tunnel** — a TUN adapter, not a per-application setting. TCP
  and UDP both go through the proxy, DNS is intercepted, and QUIC works when the
  proxy carries UDP.
- **Routing you can see** — all programs, all except the ones you pick, or only
  the ones you pick. Sites direct, sites always through the proxy, addresses
  direct, local network direct, Russian sites direct.
- **Masking** — the handshake to the proxy leaves in pieces, so a provider that
  reads the destination address out of it finds nothing to match. This is what
  makes Telegram work on networks where a plain proxy connection dies. See below.
- **Kill switch** — while it is armed, nothing leaves the machine outside the
  adapter. If the engine dies the traffic stops rather than falling back to the
  open network. Windows only for now.
- **System proxy mode** — no service, no administrator rights, for programs that
  read the system proxy and for running beside another VPN.
- **Your proxies, measured** — every proxy is probed before it is used. Login,
  whether its UDP relay really answers, the country its exit reports.
- **Your Proxya account** — active datacenter, ISP and mobile orders appear in
  the app, and residential proxies are generated against your GB balance.
- **Three languages** — English, Russian and Chinese, switched without a restart.

<p align="center">
  <img src="public/screenshots/home.png" width="360" alt="Proxya Desktop SOCKS5 proxy client for Windows and macOS: main screen with proxy selection and connection controls">
</p>

## Generate residential proxies in the app

Sign in to your Proxya account to generate residential SOCKS5 proxies directly
from your traffic balance. Choose a country, keep one IP for a selected period
or use IP rotation, and enable UDP when needed. Click **Get and connect** to
generate a proxy and connect, or add it to **My proxies** for later.

Your remaining residential traffic is shown in the same screen. Generation
requires residential traffic on your Proxya account; you can also use your own
SOCKS5 or HTTP proxies without signing in.

<p align="center">
  <img src="public/screenshots/residential.png" width="360" alt="Generate residential proxies in Proxya Desktop: country selection, sticky IP or rotation, UDP and Get and connect">
</p>

## App routing and settings

Choose which applications and websites use the proxy, keep local traffic
direct, and configure DNS, the Windows kill switch and startup behavior.

<p align="center">
  <img src="public/screenshots/routing.png" width="320" alt="Proxya Desktop split tunneling: proxy routing by application, website and IP address">
  <img src="public/screenshots/settings.png" width="320" alt="Proxya Desktop settings: Windows kill switch, startup options and DNS server selection">
</p>

## Masking

A plain proxy connection is readable. The SOCKS5 handshake carries the
destination address in clear text, and so does the `CONNECT` line of an HTTP
proxy. A provider that inspects traffic reads that address straight out of the
stream, even though the stream is going to a proxy.

This is not a theory. Measured against one Russian provider, against the
Telegram data centres, over the same proxy and the same link, in a single
packet:

| | Connections that completed |
| --- | --- |
| Handshake in one packet | 1 of 6 |
| Handshake split in two, 10 ms apart | 6 of 6 |

TLS to ordinary sites through that same proxy was never touched, which is why
only Telegram appeared broken while everything else worked.

Masking sends the handshake as two TCP segments with a pause between them. The
address is never present in a single packet, so a rule that matches on one
packet has nothing to match. The proxy itself is unaware anything happened,
which is why this works with every proxy rather than only with ours.

UDP is untouched by it. The association is handed over to the proxy as it is and
the datagrams go straight there, so a residential proxy with UDP keeps its speed.

### What masking is not

It is not encryption, and it is not sold as one. The link to a plain proxy
cannot be encrypted at all, because the proxy on the other end speaks nothing
but clear text. Measured on our own supplier: the HTTP port answers a TLS
handshake with plain text and the SOCKS port closes the connection.

So a provider still sees that you hold a connection to a proxy, and the proxy
login and password still travel in clear text, as they do with every SOCKS5 and
HTTP proxy in existence. Masking defeats a rule that reads one packet. It does
not defeat an observer who reassembles the whole stream. If you need the link
itself to be unreadable, you need an endpoint that holds a key, which means a
server of your own.

## Tunnel or system proxy

**Tunnel** installs a service that runs with the rights a TUN adapter needs. The
service builds the engine configuration itself from fields it has checked, so
another process cannot hand a privileged service a configuration of its own.
Everything on the machine goes through the proxy, including programs that have
no proxy setting at all.

**System proxy** needs no service and no administrator rights. It writes the
system proxy settings and restores them on disconnect, including after a crash.
It reaches only the programs that read those settings, and by its nature it does
not carry UDP or WebRTC. The app says so rather than hiding it.

## DNS

With a DNS server chosen, names are resolved over DoH through the proxy itself
and the proxy is handed an address. The resolver sees the proxy, not you.

With **No DNS**, the name is handed to the proxy and the proxy resolves it. That
is one fewer round trip, and it is the right answer for a rotating residential
exit, but the name travels in the handshake in clear text.

On macOS the service takes over the system DNS while the tunnel is up and puts
the previous servers back on disconnect, with a copy on disk so a crash cannot
leave the machine pointing at an adapter that no longer exists. Without that,
macOS keeps asking the router and every name you look up leaves the tunnel.

## UDP and QUIC

Before connecting, the service probes the proxy. A proxy that relays UDP to
names carries QUIC as it is. A proxy that relays UDP only to addresses gets
names resolved through DoH first. A proxy with no UDP path gets UDP closed
outright, so the browser falls back to TCP and WebRTC reveals nothing.

There is no setting that lets UDP out around the proxy, and there will not be
one. The product exists for the opposite reason.

## Honest limits

- The kill switch is Windows only. On macOS it is hidden rather than shown as a
  switch that does nothing.
- Running beside another VPN that claims the system DNS, Tailscale with its own
  resolver for example, means that resolver wins and ours does not. Two tunnels
  on one machine is a conflict, not a bug, and system proxy mode is the way to
  work next to one.
- A proxy that filters ports filters them for us too. Ports 25, 22 and a short
  list of others are closed on most commercial proxies, and a SOCKS5 proxy
  answers "succeeded" before it knows whether the port is reachable, so a
  blocked port looks like a connection that dies two minutes later.
- IPv6 through a proxy that has no IPv6 of its own will answer and then die. The
  app keeps IPv6 off by default for that reason.
- Builds are not signed yet. SmartScreen and Gatekeeper will say so. Verify the
  checksum published with the release.

## Install

Download the latest build from
[Releases](https://github.com/ProxyaAnty/Proxya-Desktop/releases/latest).

- **Windows x64** — run the installer. The tunnel mode asks for administrator
  rights once, to install the service.
- **macOS Apple Silicon** — see [Install on macOS](docs/mac-installation.md) for
  the one-time Gatekeeper step, in [Russian](docs/mac-установка.md) as well.

An account is optional. Any SOCKS5 or HTTP proxy works without signing in.

## Security and integrity

Proxy passwords and the account session are encrypted on disk with a key kept in
the operating system credential store, so copying the files out of the data
folder is not enough to read them.

The service checks that the program talking to it over the local channel is the
application it expects, and the application checks that the service on the other
end is the real one.

Report anything security related privately. See [SECURITY.md](SECURITY.md).

## What is in this repository

Documentation, installation guides, the issue tracker and the release
binaries. The application source is not published here.

```
docs/           Installation guides
public/         Icon and screenshots
.github/        Issue templates and the pull request template
```

Screenshots in this repository use demonstration data. Addresses come from the
ranges reserved for documentation, so nothing in them points at a live proxy.

## Third-party components

The tunnel engine is [sing-box](https://github.com/SagerNet/sing-box), licensed
under GPL-3.0. We ship an unmodified upstream release, verified by its published
SHA-256 at build time, and the licence travels with the installer. Its source is
available from the upstream project.

---

© 2026 Proxya
