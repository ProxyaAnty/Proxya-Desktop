# Contributing

This repository accepts changes to the documentation and the installation
guides. The desktop application and its tunnel service are maintained in a
separate private tree and are not part of the contribution surface.

## Issues are the useful contribution

A good report about the tunnel is worth more than a documentation fix. What
helps most:

- the platform and version, the connection mode, and whether a kill switch or
  another VPN was running,
- what the proxy is, as a type rather than an address. SOCKS5 or HTTP,
  datacenter, ISP, residential or mobile, with or without UDP,
- what you expected and what happened, with the tunnel log if you have it.
  **Settings, Copy the tunnel log** puts it on the clipboard,
- for anything that looks like a leak, how you observed it.

Never paste real proxy credentials, account data or a live session into an
issue. An address from a documentation range is enough to describe a shape.

## Before opening a pull request

1. Do not include tokens, account data, proxy credentials or binaries.
2. Keep the guides accurate for both platforms, or say plainly which one a step
   applies to.
3. Explain the user-visible change.

Screenshots must use demonstration data from the ranges reserved for
documentation.
