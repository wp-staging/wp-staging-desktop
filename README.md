# WP Staging Desktop

**Create and manage local WordPress sites from a desktop app.**

WP Staging Desktop is a desktop app for creating and managing local WordPress sites. Spin up isolated WordPress development environments, manage containers, view logs, and restore `.wpstg` backups -- all from one app on **Windows, macOS, or Linux**.

Built for developers and agencies who value their time.

> **License Required:**
> A valid [WP Staging Agency or Developer license](https://wp-staging.com) is required.

---

## Highlights

- **Site management** -- Start, stop, create, reset, rename, and delete WordPress Docker containers from a graphical interface.
- **Real-time terminal** -- Live output stream with auto-scroll, color-coded log lines, and inline copy/clear.
- **Backup restore** -- Restore `.wpstg` backups through the UI without typing commands.
- **System status** -- Live RAM, CPU, and disk usage in the status bar.
- **Native installers** -- Signed and notarized on macOS, signed via Microsoft on Windows, portable AppImage on Linux.

---

## Installation

Download the installer for your platform from the latest release on this repository's [Releases page](https://github.com/wp-staging/wp-staging-desktop/releases).

### macOS

1. Download `wpstaging-desktop-{version}-mac-universal.dmg`.
2. Open the DMG and drag **WP Staging Desktop** into Applications.
3. Launch from Applications. macOS Gatekeeper recognizes the signed app automatically.

The DMG is signed with a Developer ID certificate and notarized by Apple. It runs natively on both Intel and Apple Silicon Macs.

### Linux

1. Download `wpstaging-desktop-{version}.AppImage`.
2. Make it executable: `chmod +x wpstaging-desktop-*.AppImage`.
3. Run it: `./wpstaging-desktop-*.AppImage`.

No installation step is needed -- the AppImage is portable.

### Windows

Two Windows builds are available once a release ships:

- **Installer** -- `wpstaging-desktop-{version}-win-x64-setup.exe`. Standard install with Start menu entry and uninstaller in **Settings > Apps**.
- **Portable** -- `wpstaging-desktop-{version}-win-x64-portable.exe`. Self-contained, no install. Useful when you do not have admin rights, are on a locked-down work machine, or just prefer running from a folder you control.

A signed Windows release is in preparation. See the [Releases page](https://github.com/wp-staging/wp-staging-desktop/releases) for status.

### First launch

The first time you open the app, it downloads the wpstaging engine -- the local component that powers site creation and management -- and saves it to your user folder. You will see a one-time progress screen. No administrator password is needed. The wpstaging engine is also reinstalled automatically if the file ever goes missing.

---

## Requirements

See [docs/SYSTEM-REQUIREMENTS.md](docs/SYSTEM-REQUIREMENTS.md) for the full list of supported operating systems, Docker, and hardware requirements.

---

## Documentation

- [System Requirements](docs/SYSTEM-REQUIREMENTS.md) -- supported OS, Docker, hardware, internet, common problems.
- [FAQ](docs/FAQ.md) -- frequently asked questions for end users.

---

## Support

For help, please visit [wp-staging.com/support](https://wp-staging.com/support/).

---

## License

The WP Staging Desktop GUI source code is source-available under the WP STAGING Desktop GUI Source-Available License (see the `LICENSE.md` and `NOTICE.md` files). The WP Staging Desktop Core (WP Staging Engine), license validation logic, entitlement system, activation service, update service, Pro feature execution logic, official distributed binaries, and cloud services are proprietary components. Third-party components remain governed by their own licenses. A valid [WP Staging Agency or Developer license](https://wp-staging.com) is required to use Pro features -- see your license agreement at [wp-staging.com](https://wp-staging.com) for terms.
