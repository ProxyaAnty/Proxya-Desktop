# Install Proxya Desktop on Windows

## Install

1. Download `Proxya_1.0.0_x64-setup.exe` from
   [Releases](https://github.com/ProxyaAnty/Proxya-Desktop/releases/latest) and
   verify its SHA-256 against the value published with the release.
2. Run the installer. It installs for the whole machine, into
   `C:\Program Files\Proxya`.
3. Builds are not Authenticode signed yet, so SmartScreen can show an unknown
   publisher. Check the checksum first, then choose **More info, Run anyway**.

## The tunnel service

Tunnel mode needs a Windows service that runs as SYSTEM, because that is what a
TUN adapter requires. The installer registers it and Windows asks for
confirmation once. System proxy mode needs neither the service nor those
rights.

## The kill switch

While the kill switch is armed, filters on the Windows Filtering Platform block
everything that does not come from the Proxya adapter, except the engine and
the service, loopback, DHCP and, if you allow it, the local network. If the
engine dies, the adapter disappears and the traffic stops instead of falling
back to the open network.

The filter session is dynamic. If the service itself stops, Windows removes the
filters, so the machine is never left without a network.

## Running beside another VPN

Two tunnels with strict routing on one machine break each other's DNS. That is
expected rather than a bug. Use system proxy mode beside another VPN.

## Where data lives

`%APPDATA%\Proxya`. Proxy passwords and the account session are encrypted with
a key held in Windows Credential Manager, so copying the folder to another
machine does not carry account access or proxy passwords with it.
