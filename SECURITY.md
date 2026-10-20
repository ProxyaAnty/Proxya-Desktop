# Security policy

## Supported releases

Security fixes are applied to the current desktop release.

## Report a vulnerability privately

Do not open a public issue for vulnerabilities, leaked credentials, a bypass of
the tunnel, or a finding that includes customer data. Contact Proxya through
[proxya.co/contact](https://proxya.co/contact) and include:

- the affected version and platform,
- a minimal reproduction without real account or proxy credentials,
- the expected impact,
- whether the finding has been shared elsewhere.

We will acknowledge a complete report, reproduce it, and agree a fix and
disclosure timeline with you. Please do not access data that is not yours,
degrade the service, or run high-volume tests against production.

## What counts as a leak

Anything that leaves the machine outside the tunnel while the tunnel is up is
treated as a security bug rather than a feature request. That includes DNS
queries, UDP, WebRTC candidates and traffic from a program that routing was
supposed to cover. If you can show a packet going around the proxy, we want to
know.

## Release integrity

Release assets are published with their SHA-256. Builds are not code signed
yet, so an operating system warning about an unknown publisher is expected.
Verify the checksum before running an installer. If an asset does not match its
published checksum, do not run it and report the mismatch privately.

The application source is not part of this repository.
