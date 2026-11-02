# System Requirements

This page lists what you need on your computer to install and use WP Staging Desktop.

---

## Quick Check

Before you install, make sure you have:

- A supported operating system (see the table below).
- Docker installed and running.
- An internet connection for the first run.
- 4 GB of RAM or more.
- 10 GB of free disk space or more.

If all of these are true, you are ready to install.

---

## Supported Operating Systems

We provide a signed app for macOS and Windows. The Linux AppImage is not signed.

| System | Version you need | Download file |
|--------|------------------|----------------|
| macOS | 13 (Ventura) or newer | `.dmg` (contains the `.app` -- drag to Applications) |
| Windows | Windows 10 or newer (also Windows Server 2019+) | `.exe` installer, or a portable `.exe` (no install needed) |
| Linux | Ubuntu 20.04 or newer, Debian 11+, Fedora 32+, RHEL 9+ | `.AppImage` (portable, no install needed) |

The macOS app is a universal build. It works on both Intel Macs and Apple Silicon Macs (M1, M2, M3, and so on).

The Windows app is for 64-bit Windows only. The portable `.exe` does not update itself. To update it, download the new file by hand.

The Linux app is for 64-bit Linux only.

Older systems are not supported.

**Older systems:** WP Staging Desktop 1.7.1 is the last version that supports macOS 11 (Big Sur) and macOS 12 (Monterey). If you use one of these systems, download [version 1.7.1](https://github.com/wp-staging/wp-staging-desktop/releases/tag/v1.7.1). It does not get new features or fixes.

---

## Docker

WP Staging Desktop builds local WordPress sites inside Docker. You must install Docker before you can create sites.

### Recommended

**Docker Desktop** is the easiest choice on all three systems. Download it from [docker.com](https://www.docker.com/products/docker-desktop/).

After you install Docker Desktop, open it once so it starts running. The Docker badge at the top of WP Staging Desktop shows when Docker is ready.

### Other tools we detect

We can see if you have these tools, but creating sites only works fully with Docker Desktop or Docker Engine:

| Tool | Works for sites? | Notes |
|------|------------------|-------|
| Docker Desktop | Yes | Best choice. |
| Docker Engine (Linux only) | Yes | A good choice if you do not want Docker Desktop. |
| OrbStack | No | We can show its status, but sites will not start. OrbStack does not support the network setup our sites need. |
| Rancher Desktop | Partly | Status shows in the badge. Site creation is not tested. |
| Colima | Partly | Status shows in the badge. Site creation is not tested. |
| Podman Desktop | Partly | Status shows in the badge. Site creation is not tested. |

### Docker version

You need Docker 20.10 or newer. To check, open a terminal and run:

```
docker version
```

If the version is older, please update Docker.

---

## License

You do not need a license to use the app for local development. Without a license, you can create local sites and restore a site from a local `.wpstg` backup file.

A WP Staging Pro **Agency** or **Developer** license unlocks the Pro features, such as Remote Sync and restoring from a backup URL. Enter your license key on the **Pro** page. After the license is active, this page is called **License**. You can buy a license at [wp-staging.com](https://wp-staging.com).

With a paid license, the wpstaging engine checks the license online and keeps the result for 4 hours. After that, it checks again the next time you create, start, or change a site. **Check Status** on the License page shows the saved license details. It does not start a new online check.

---

## Computer Specifications

These are the lowest specifications that work, and the ones we recommend.

### Lowest that works

- 2 CPU cores
- 4 GB of RAM
- 10 GB of free disk space
- Broadband internet (5 Mbps or faster)

### What we recommend

- 4 CPU cores or more
- 8 GB of RAM or more
- 20 GB of free disk space, on an SSD if possible
- Broadband internet (25 Mbps or faster)

Each WordPress site you create uses about 500 MB of disk space and 100 to 300 MB of memory while it is running. If you plan to run many sites at once, more RAM helps.

---

## Internet Connection

The app needs the internet at certain times:

| When | Why |
|------|-----|
| First launch | To download the wpstaging engine (one-time) |
| First time you enter your license | To check it with our server |
| With a paid license, when you create, start, or change a site (at most once every 4 hours) | To check your license |
| First time you create a site | To download Docker images |
| Each time you start the app, and every six hours after that | To get the list of recent WordPress versions |
| Each time you start the app, and every 4 hours after that | To check GitHub for a new version of the app |
| Each time you start the app | To check GitHub for a new wpstaging engine version (at most once a day) |
| Each time you start the app | To load announcements from wp-staging.com |
| When the app installs or updates the wpstaging engine | To tell wp-staging.com that the engine was installed |
| When you send a Help & Feedback message | To send your message to wp-staging.com |

The wpstaging engine is not packaged with the app. The first time you launch WP Staging Desktop, an onboarding screen downloads the wpstaging engine from the official release and saves it under your user folder. If the file is ever removed, the app reinstalls the wpstaging engine automatically on the next status check. The app checks for a new version of itself when it starts and every 4 hours. It downloads and installs a new version only after you click. See the FAQ question "How do I update the app?" in [FAQ.md](FAQ.md#q39).

After Docker images are downloaded, you can use most of the app offline. A paid license needs the internet again for its check every 4 hours. You will only need the internet again to create a new site with images you do not have yet.

---

## Where Files Are Stored

The first time you use the app, it creates a folder in your home folder for your WordPress sites:

| Folder | What it holds |
|--------|---------------|
| `~/wpstaging/sites/<site-name>/` | The files for one WordPress site |
| `~/wpstaging/sites/<site-name>/data/mariadb/` | The database files for that one site |
| `~/wpstaging/stack/ca/` | A local certificate used for HTTPS on local sites |
| `~/wpstaging/stack/docker/` | A few small support scripts |

If you switch on **Store the database in a Docker volume** when you create a site, that site keeps its database files inside Docker instead of the folder above.

When the app downloads the wpstaging engine, it saves it here:

| System | Engine file |
|--------|-------------|
| macOS, Linux | `~/.local/bin/wpstaging` |
| Windows | `%LOCALAPPDATA%\Programs\wpstaging\wpstaging.exe` |

The app also saves its own settings (theme, layout, license) in the standard place for your system:

| System | Settings folder |
|--------|------------------|
| macOS | `~/Library/Application Support/wpstaging-desktop/` |
| Windows | `%APPDATA%\wpstaging-desktop\` |
| Linux | `~/.config/wpstaging-desktop/` |

---

## Administrator Password

A few tasks need your administrator (admin) password. The app asks for it when needed, with the standard password window from your system. It does not stay open as admin all the time.

| Task | When the password is needed | System |
|------|----------------------------|--------|
| Add a site name to your hosts file | Every time a new site is created | macOS, Linux, Windows |
| Set up a special local network address for a site | macOS only, on first run after a reboot | macOS |
| Trust the local HTTPS certificate | Once, when you ask the app to install it | All systems |

---

## Notes for Each System

### macOS

- The app is signed by Apple, so you should not see a security warning when you open it.
- The first launch can take a few seconds while macOS finishes its checks.
- You will be asked for your password the first time the app needs to set up a network address for a site (for example, after a restart).

### Windows

- The installer is signed. Microsoft SmartScreen may still show a warning the first few times. Click **More info**, then **Run anyway** to continue. The warning will stop appearing after a few releases.
- Docker Desktop on Windows must be in **Linux container mode**. This is the default. If yours is in Windows container mode, the app will ask you if it can switch.

### Linux

- The `.AppImage` is a portable app. Mark it as executable, then double-click to start:
  ```
  chmod +x wpstaging-desktop-*-linux-x64.AppImage
  ```
- The `.AppImage` file needs a small library called **FUSE 2**. If your AppImage does not start, install it:
  - Ubuntu 22.04 or newer: `sudo apt install libfuse2`
- For non-root use of Docker, add your user to the `docker` group:
  ```
  sudo usermod -aG docker $USER
  ```
  Then log out and log back in.

---

## Common Problems

**The app does not open on macOS, and it says the developer cannot be verified.**
You may have an unsigned copy. Please download the installer again from the official release page.

**Microsoft SmartScreen blocks the installer on Windows.**
Click **More info**, then **Run anyway**. This is normal for new apps until they build up a reputation with Microsoft.

**The Docker badge says Docker is not running.**
Open Docker Desktop (or your other Docker tool) and wait until it shows it is ready. The badge at the top of the app will update on its own.

**Sites will not start when I use OrbStack.**
OrbStack does not support the network setup we need. Switch to Docker Desktop by opening a terminal and running:
```
docker context use desktop-linux
```

**The Linux AppImage does not start (FUSE error).**
Install FUSE 2: `sudo apt install libfuse2` on Ubuntu or Debian.

**I see a warning that the hosts file could not be updated.**
This means the password window was closed without entering your password, or your user does not have admin rights. Try the action again and enter your password when asked.

**The status bar shows low disk space.**
Free space on the drive that holds the `~/wpstaging/` folder. To remove old Docker images you no longer use, open a terminal and run:
```
docker system prune -a
```

---

## More Help

- **[wp-staging.com](https://wp-staging.com)** -- Prices, plans, and product information.
- **[wp-staging.com/support](https://wp-staging.com/support)** -- Get help from our support team.

---

**Last Updated:** 2026-10-18 15:12:32 UTC
