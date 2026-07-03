# System Requirements

This page lists what you need on your computer to install and use WP Staging Desktop.

---

## Quick Check

Before you install, make sure you have:

- A supported operating system (see the table below).
- Docker installed and running.
- A WP Staging Pro license key.
- An internet connection for the first run.
- 4 GB of RAM or more.
- 10 GB of free disk space or more.

If all of these are true, you are ready to install.

---

## Supported Operating Systems

We provide a signed app for each system.

| System | Version you need | Download file |
|--------|------------------|----------------|
| macOS | 11 (Big Sur) or newer | `.dmg` (contains the `.app` -- drag to Applications) |
| Windows | Windows 10 or newer (also Windows Server 2019+) | `.exe` installer |
| Linux | Ubuntu 20.04 or newer, Debian 11+, Fedora 32+, RHEL 8+ | `.AppImage` (portable, no install needed) |

The macOS app is a universal build. It works on both Intel Macs and Apple Silicon Macs (M1, M2, M3, and so on).

The Windows app is for 64-bit Windows only.

The Linux app is for 64-bit Linux only.

If your system is older, the app will not start.

---

## Docker

WP Staging Desktop builds local WordPress sites inside Docker. You must install Docker before you can create sites.

### Recommended

**Docker Desktop** is the easiest choice on all three systems. Download it from [docker.com](https://www.docker.com/products/docker-desktop/).

After you install Docker Desktop, open it once so it starts running. The status bar at the bottom of WP Staging Desktop shows when Docker is ready.

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

You need a valid WP Staging Pro license. Both the **Agency** and **Developer** licenses work.

Enter your license key on the License page the first time you open the app. You can buy a license at [wp-staging.com](https://wp-staging.com).

The app checks your license online once after Docker becomes available on each app start, and remembers the result until you restart the app. To re-check sooner, open the License page and click **Check status**.

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
| Each time you start the app, after Docker is up | To verify your license once per session |
| First time you create a site | To download Docker images |
| Every six hours while the create-site window is open | To get the list of recent WordPress versions |

The wpstaging engine is not packaged with the app. The first time you launch WP Staging Desktop, an onboarding screen downloads the wpstaging engine from the official release and saves it under your user folder. If the file is ever removed, the app reinstalls the wpstaging engine automatically on the next status check. The app does not poll for its own updates today; new releases are installed manually.

After Docker images are downloaded and your license is checked on start, you can use most of the app offline. You will only need the internet again to create a new site with images you do not have yet.

---

## Where Files Are Stored

The first time you use the app, it creates a folder in your home folder for your WordPress sites:

| Folder | What it holds |
|--------|---------------|
| `~/wpstaging/sites/<site-name>/` | The files for one WordPress site |
| `~/wpstaging/stack/mariadb/` | The database storage shared by all sites |
| `~/wpstaging/stack/ca/` | A local certificate used for HTTPS on local sites |
| `~/wpstaging/stack/docker/` | A few small support scripts |

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
  chmod +x WP-STAGING-Desktop-*.AppImage
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
Click **More info**, then **Run anyway**. This is normal for new signed apps until they build up a reputation.

**The status bar says Docker is not running.**
Open Docker Desktop (or your other Docker tool) and wait until it shows it is ready. The status bar will update on its own.

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

**Last Updated:** 2026-05-31 02:38:13 UTC
