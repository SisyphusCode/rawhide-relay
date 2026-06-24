# Boulder Relay

A GTK4 IRC client built in Rust using [relm4](https://relm4.org/), tuned for the Rocky Linux community on Libera.Chat.

Named for the Sisyphus myth — the conversation you keep pushing uphill.

## Features

- TLS IRC connection (port 6697)
- NickServ authentication (required for Rocky Linux channels)
- Multi-channel support with live user lists
- Channel favorites and per-user mute
- Persistent settings (`~/.config/boulder-relay/settings.conf`)
- Connect / disconnect controls
- Timestamps and auto-scrolling chat view
- Slash commands: `/join`, `/msg`, `/nick`
- Gruvbox Dark theme with Rocky green accents

## Default channels

On connect, the client joins Rocky Linux community channels on `irc.libera.chat`:

| Channel | Purpose |
|---------|---------|
| `#rockylinux` | General support and discussion |
| `#rockylinux-devel` | Development and release engineering |
| `#rockylinux-social` | Off-topic and social chat |

See the [Rocky Linux IRC wiki](https://wiki.rockylinux.org/irc/) for the full channel list and NickServ registration steps.

## Install from COPR

```bash
sudo dnf copr enable sisyphuscode/boulder-relay
sudo dnf install boulder-relay
```

Builds are provided for **EPEL 9**, **EPEL 10**, and Fedora Rawhide.

On RHEL 10 / Rocky Linux 10 / Alma 10, enable EPEL 10 first if it is not already enabled.

## Development setup

Install build dependencies on Rocky Linux 9 / 10:

```bash
sudo dnf install -y cargo rust gtk4-devel openssl-devel desktop-file-utils libappstream-glib
```

The project pins `relm4 0.8` / `gtk4 0.8` (with default features disabled) so it builds against the GLib and Pango libraries shipped on EL9 and EL10.

Build and run locally:

```bash
cargo run
```

Build an RPM (offline, using vendored crates):

```bash
./packaging/build-rpm.sh
```

Or manually:

```bash
cargo build --release --offline
rpmbuild -ba packaging/boulder-relay.spec
```

Refresh vendored sources after dependency changes:

```bash
cargo vendor vendor
```

## Dependencies

- Rust + Cargo
- GTK4 development libraries (`gtk4-devel`)
- OpenSSL development libraries (`openssl-devel`)

## License

GPL-2.0-or-later
