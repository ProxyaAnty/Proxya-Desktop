# Install Proxya Desktop on macOS

The build supports Apple Silicon. It is ad-hoc signed and not notarized with an
Apple Developer ID, so Gatekeeper can say that the developer cannot be verified
or that the application is damaged after download.

## Install

1. Download `Proxya-macos-arm64.tar.gz` from
   [Releases](https://github.com/ProxyaAnty/Proxya-Desktop/releases/latest) and
   verify its SHA-256 against the value published with the release.
2. Extract it and move **Proxya** into **Applications**.
3. In Terminal, once:

   ```bash
   xattr -dr com.apple.quarantine "/Applications/Proxya.app"
   ```

4. Open Proxya normally.

If you would rather not use Terminal, try to open the application once, then go
to **System Settings, Privacy and Security** and choose **Open Anyway**.

## The tunnel service

Tunnel mode needs a small service that runs with the rights a TUN adapter
requires. The application installs it on first use and macOS asks for your
administrator password at that moment. Nothing else in the application asks for
it.

To remove the service later:

```bash
sudo "/Applications/Proxya.app/Contents/MacOS/proxya-service" uninstall
```

System proxy mode needs no service and no password.

## While the tunnel is up

The service points the system DNS at the tunnel and puts your previous servers
back when you disconnect. A copy of the previous settings is kept on disk, so a
crash cannot leave the Mac pointing at an adapter that is no longer there.

If another VPN on the Mac manages DNS itself, Tailscale with its own resolver
for example, that resolver stays in front of ours and names will be resolved
outside the tunnel. Two tunnels on one machine is a conflict rather than a bug.
Turn the other one off, or use system proxy mode beside it.

## The kill switch

The kill switch is Windows only for now. On macOS it is hidden rather than
offered as a switch that does nothing.

## Where data lives

`~/Library/Application Support/Proxya` for the application, and
`/Library/Application Support/Proxya` for the service. Proxy passwords and the
account session are encrypted with a key held in the macOS Keychain, so copying
the folder to another Mac does not carry account access or proxy passwords with
it.
