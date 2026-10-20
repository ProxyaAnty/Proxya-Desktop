# Proxya Desktop binary licence

The documentation and guides in this repository are licensed under MIT.
**The Proxya Desktop application, its tunnel service and its configuration are
not covered by MIT.**

Those proprietary components are distributed separately in compiled form.
Subject to an active Proxya account where one is required, you may install and
run them for lawful personal or commercial use. You may not redistribute,
resell, sublicense or offer the binaries as a standalone product, bypass or
remove licence or integrity checks, extract proprietary components for use in
another product, or reverse engineer them except where applicable law gives a
non-waivable right to do so.

## Third-party components

This licence does not restrict rights granted by third-party licences.

The tunnel engine is [sing-box](https://github.com/SagerNet/sing-box) by
SagerNet, licensed under **GPL-3.0**. Proxya Desktop ships an unmodified
upstream release of it as a separate executable and invokes it as a child
process. The GPL-3.0 licence text is installed alongside the application, and
the complete corresponding source is available from the upstream project at
<https://github.com/SagerNet/sing-box>. The build pipeline downloads the
release from that project and verifies its published SHA-256 before use.

Routing rule sets are built from the sing-geoip and sing-geosite projects and
carry their own licences.

The binaries are provided without warranties to the maximum extent permitted by
law. Questions and commercial licensing: <https://proxya.co/contact>
