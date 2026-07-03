# WP Staging Desktop FAQ

## General Questions

<a name="q1"></a>
**Q1: What is WP Staging Desktop?**  
**A1:**
WP Staging Desktop is a desktop app for Windows, macOS, and Linux. It lets you create and manage local WordPress sites on your own computer with a few clicks.

<a name="q2"></a>
**Q2: Which operating systems are supported?**  
**A2:**
macOS 11 (Big Sur) or newer, Windows 10 or newer, and 64-bit Linux (Ubuntu 20.04+, Debian 11+, Fedora 32+, RHEL 8+). Older systems will not start the app.

<a name="q3"></a>
**Q3: Do I need a license to use this app?**  
**A3:**
Yes. You need a valid WP Staging Pro license (Agency or Developer). You can buy one at [wp-staging.com](https://wp-staging.com).

<a name="q4"></a>
**Q4: Is the app free?**  
**A4:**
The app itself is free to download. To use it, you need a paid WP Staging Pro license.

<a name="q5"></a>
**Q5: Does this replace the WP Staging WordPress plugin?**  
**A5:**
No. The plugin runs inside your live WordPress site. WP Staging Desktop runs on your own computer to create local test sites. The two work together but solve different problems.

<a name="q5a"></a>
**Q5a: What is the WP Staging Engine?**  
**A5a:**
The WP Staging Engine is the [WP Staging CLI](https://github.com/wp-staging/wp-staging-cli-release), scoped and enhanced to power WP Staging Desktop. It does the heavy lifting for your local sites — creating sites, starting and stopping containers, issuing auto-login URLs, and more. You do not run it yourself; the app drives it behind the scenes and keeps it up to date. The binary file is named `wpstaging`, so in technical messages you may see it called the "wpstaging engine".

<a name="q6"></a>
**Q6: Does it support Apple Silicon Macs (M1, M2, M3)?**  
**A6:**
Yes. The macOS app is a universal build. It works on both Intel Macs and Apple Silicon Macs.

<a name="q7"></a>
**Q7: Is there a 32-bit version?**  
**A7:**
No. The app is 64-bit only on all systems.

---

## Installation Questions

<a name="q8"></a>
**Q8: How do I install it?**  
**A8:**
Download the file for your system from the official release page and run it.

- macOS: open the `.dmg` and drag the app to your Applications folder.
- Windows: run the `.exe` installer.
- Linux: the `.AppImage` is a portable app. Mark it as executable (`chmod +x WP-STAGING-Desktop-*.AppImage`), then double-click to start.

<a name="q8a"></a>
**Q8a: What happens the first time I launch the app?**  
**A8a:**
The app shows a one-time onboarding screen. It downloads the wpstaging engine from the official release and saves it to your user folder. The screen shows a progress bar and confirms the file with a SHA-256 check before saving it.

The file is saved under your own user folder, so no administrator password is needed:

- macOS / Linux: `~/.local/bin/wpstaging`
- Windows: `%LOCALAPPDATA%\Programs\wpstaging\wpstaging.exe`

After this one-time step, the main app opens. If `wpstaging` is already on your computer, the app uses your existing copy and skips this step.

<a name="q8b"></a>
**Q8b: What if the wpstaging engine file is deleted or missing?**  
**A8b:**
The app notices on the next status check and shows the onboarding screen again. It downloads a fresh copy automatically. You do not need to reinstall the whole app.

<a name="q9"></a>
**Q9: Why does macOS say "the developer cannot be verified"?**  
**A9:**
You may have an unsigned copy. Please download the installer again from the official release page. The official build is signed and notarized by Apple, so this warning should not appear.

<a name="q10"></a>
**Q10: Why does Microsoft SmartScreen warn me on Windows?**  
**A10:**
The installer is signed, but SmartScreen builds trust over time. The warning will stop after a few releases. To continue, click **More info**, then **Run anyway**.

<a name="q11"></a>
**Q11: My Linux AppImage will not start. It says something about FUSE.**  
**A11:**
AppImage needs the FUSE 2 library. On Ubuntu or Debian, install it with `sudo apt install libfuse2`. Then try the AppImage again.

<a name="q12"></a>
**Q12: Can I install the app on a server without a desktop?**  
**A12:**
No. The app needs a graphical desktop. For headless servers, use the [WP Staging CLI](https://github.com/wp-staging/wp-staging-cli-release) instead.

<a name="q13"></a>
**Q13: How do I uninstall the app?**  
**A13:**

- macOS: drag the app from Applications to the Trash.
- Windows: open **Settings** > **Apps** and remove **WP Staging Desktop**.
- Linux: delete the `.AppImage` file.

Your sites in `~/wpstaging/` are not removed. Delete that folder yourself if you want a full cleanup.

---

## Docker Questions

<a name="q14"></a>
**Q14: Do I need Docker?**  
**A14:**
Yes. The app uses Docker to run each WordPress site in its own small environment. Without Docker, you cannot create sites.

<a name="q15"></a>
**Q15: Which Docker should I install?**  
**A15:**
We recommend **Docker Desktop**. It works on macOS, Windows, and Linux. Download it from [docker.com](https://www.docker.com/products/docker-desktop/).

<a name="q16"></a>
**Q16: I have OrbStack. Can I use it?**  
**A16:**
You can see its status in the app, but sites will not start under OrbStack. OrbStack does not support the local network setup our sites need. Switch to Docker Desktop or Docker Engine.

<a name="q17"></a>
**Q17: What about Rancher Desktop, Colima, or Podman Desktop?**  
**A17:**
The app can show the status of these tools. Site creation has not been tested with them. We only fully support Docker Desktop and Docker Engine.

<a name="q18"></a>
**Q18: How do I know Docker is running?**  
**A18:**
The status bar at the top of the app shows a Docker badge. When Docker is ready, the badge is green and shows the product name and version.

<a name="q19"></a>
**Q19: Which Docker version do I need?**  
**A19:**
Docker 20.10 or newer. To check, open a terminal and run `docker version`. If your version is older, please update Docker.

<a name="q20"></a>
**Q20: Does it work with Windows containers?**  
**A20:**
No. Docker Desktop on Windows must be in **Linux container mode** (the default). If you are in Windows container mode, the app will ask if it can switch for you.

---

## Using the App

<a name="q21"></a>
**Q21: How do I create my first site?**  
**A21:**
Click the **Create site** button at the top of the app. Enter a name, pick a PHP and WordPress version, and click **Create**. The app downloads the needed images the first time, then sets up the site for you.

<a name="q21a"></a>
**Q21a: How do I change the PHP or WordPress version for an existing site?**  
**A21a:**
Open the site detail page and go to the **PHP / WP** tab. Pick a new version from **Switch PHP version** or **Switch WordPress version**, click **Switch**, and confirm the change. The site must be running.

- Switching PHP restarts only this site's containers. The site is offline for a few seconds. Other sites are not affected.
- Switching WordPress replaces the core files in place. The database, plugins, themes, and uploads are preserved. Containers do not restart.

<a name="q22"></a>
**Q22: Where are my sites stored?**  
**A22:**
In your home folder, under `~/wpstaging/sites/<site-name>/`. The shared database files live in `~/wpstaging/stack/mariadb/`.

<a name="q23"></a>
**Q23: How do I open a site in my browser?**  
**A23:**
On the site card, click **Open**. The app opens the site URL in your default browser. The site URL is also shown on the site detail page.

<a name="q24"></a>
**Q24: How do I log in to wp-admin?**  
**A24:**
On the site detail page, click **Open wp-admin**. The credentials are shown on the same page under **Admin user** and **Admin password**.

<a name="q25"></a>
**Q25: Can I see emails sent by my local site?**  
**A25:**
Yes. Each site has a built-in mail viewer called **Mailpit**. Click the Mailpit button on the site detail page to open it.

<a name="q26"></a>
**Q26: How do I delete a site?**  
**A26:**
On the site detail page, scroll to the **Danger zone** at the bottom and click **Delete site**. You must confirm twice. This removes the site files and its database.

<a name="q27"></a>
**Q27: My site shows an HTTPS warning in the browser. How do I fix it?**  
**A27:**
Open the **Settings** page in the app and click **Install local certificate authority**. Enter your password when asked. The next time you open the site, the warning is gone.

<a name="q27a"></a>
**Q27a: Only one of my sites has a certificate warning. How do I fix just that site?**  

**A27a:**
Open the site, then click the **Diagnose** tab. Find the **Site Certificate** row. If it shows expired, stale, or not trusted, click **Reinstall Certificate** under the **Suggested fix** box. The app reissues this site's certificate and restarts its containers. Other sites and the local certificate authority are not changed.

<a name="q28"></a>
**Q28: What is the terminal panel at the bottom of the app?**  
**A28:**
It shows what the underlying tool is doing. You can copy the text or hide the panel. Power users can read the panel to see the exact commands the app runs.

<a name="q29"></a>
**Q29: Can I switch between sidebar and top navigation?**  
**A29:**
Yes. Click the layout toggle in the header. Your choice is saved.

<a name="q30"></a>
**Q30: Does the app have a dark mode?**  
**A30:**
Yes. Click the theme button in the header to switch between **Light**, **Dark**, and **Auto** (follows your system setting).

<a name="q31"></a>
**Q31: Can I restore a backup made by the WP Staging WordPress plugin?**  
**A31:**
Yes. When creating a site, click **Advanced options** and pick your `.wpstg` backup file with the **Restore from backup** picker. The new site is built from your backup.

<a name="q31a"></a>
**Q31a: Where do restored backups go on my computer?**  
**A31a:**
The app keeps extracted and downloaded backups under a folder called **wpstaging-desktop-archive** in your home directory. To change the location, open the **Settings** page and edit **Backup Workspace**. The app creates `wpstaging-output` and `wpstaging-download` subfolders inside your chosen folder.

<a name="q32"></a>
**Q32: How do I see all running containers?**  
**A32:**
Open the **Containers** page from the sidebar (or top navigation). It shows every container that belongs to your sites, with its image, status, and ports.

---

## License Questions

<a name="q33"></a>
**Q33: How do I enter my license key?**  
**A33:**
Open the **License** page. Paste your key in the license field and click **Register**.

<a name="q34"></a>
**Q34: Does the app work offline?**  
**A34:**
Yes, most of the time. The internet is only needed the first time to download the wpstaging engine, pull the Docker images, and check your license. Once the wpstaging engine and images are cached and your license has been validated on this start-up, you can keep using the app offline until you restart it.

<a name="q35"></a>
**Q35: How long is my license remembered?**  
**A35:**
The app checks your license online once after Docker becomes available on each app start, then remembers the result on this computer until you restart the app. To force a fresh check, click **Check status** on the License page.

<a name="q36"></a>
**Q36: I see "License invalid" but I have a valid key.**  
**A36:**
Check your internet connection and try **Check status** on the License page. If the problem stays, contact [WP Staging support](https://wp-staging.com/support).

<a name="q37"></a>
**Q37: Can I use the same license on more than one computer?**  
**A37:**
Yes, up to the limit of your license type. See the plan details on [wp-staging.com](https://wp-staging.com).

<a name="q38"></a>
**Q38: How do I deactivate my license on one computer?**  
**A38:**
Open the License page and click **Deactivate**. You can then use the license on a different computer.

---

## Updates and Maintenance

<a name="q39"></a>
**Q39: How do I update the app?**  
**A39:**
Updates are manual today. To get a new version, open the [WP Staging Desktop releases page](https://github.com/wp-staging/wp-staging-desktop/releases), download the new file for your system, and then:

- macOS: open the new `.dmg` and drag the app to Applications. Choose **Replace** when asked.
- Windows: run the new installer. It will close the old app and update it for you.
- Linux: replace your old `.AppImage` with the new one. Mark the new file as executable.

Your sites are kept.

<a name="q39a"></a>
**Q39a: What are the notifications shown by the bell icon?**  

**A39a:**
The bell at the top of the app shows two kinds of messages:

- An available **wpstaging engine** update, with an Update button.
- Announcements from WP Staging, such as news, tips, or important notices.

Announcements are made for the desktop app and match your app version, so you only see messages meant for you. Dismiss an announcement to hide it. Some critical notices cannot be dismissed.

<a name="q40"></a>
**Q40: Will I lose my sites when I update?**  
**A40:**
No. Sites are stored in `~/wpstaging/`, which is not touched by the installer or the AppImage. You keep your sites between updates.

<a name="q41"></a>
**Q41: How do I free up disk space?**  
**A41:**

- Delete sites you no longer need from the site detail page.
- Remove unused Docker images by opening a terminal and running `docker system prune -a`. This removes only images that no site needs.

<a name="q42"></a>
**Q42: How do I move my sites to a new computer?**  
**A42:**
The simplest way is to use the WP Staging Pro plugin to create a backup file (`.wpstg`) on the old computer, copy it to the new one, and restore it when creating a site.

---

## Privacy and Network

<a name="q43"></a>
**Q43: What does the app send to the internet?**  
**A43:**
The app contacts a few servers:

- **wp-staging.com** to check your license and to load announcements shown in the app.
- **Docker Hub** to download container images the first time.
- **api.wordpress.org** to get the list of recent WordPress versions.

The wpstaging engine is downloaded once from the official release on first launch. After that, the wpstaging engine runs locally and the release server is not contacted again during normal use.

It does not send your site data anywhere.

<a name="q44"></a>
**Q44: Are my sites public on the internet?**  
**A44:**
No. Your sites only listen on your own computer. Other people on your network cannot reach them by default.

<a name="q45"></a>
**Q45: Why does the app ask for my password?**  
**A45:**
Some setup steps need administrator access:

- Adding the site name to your computer's hosts file.
- Setting up a local network address on macOS (after a restart).
- Trusting the local HTTPS certificate.

---

## Common Problems

<a name="q46"></a>
**Q46: The status bar says Docker is not running.**  
**A46:**
Open Docker Desktop (or your Docker tool) and wait until it shows it is ready. The status bar in the app updates by itself.

<a name="q47"></a>
**Q47: A site will not start.**  
**A47:**
First check the Docker badge. If Docker is running, open the terminal panel at the bottom and click **Start** again. The error in the panel often tells you what is wrong (a missing tool, a port already in use, or an old container).

<a name="q48"></a>
**Q48: Two sites try to use the same port.**  
**A48:**
The app picks a free port for each new site, but sometimes a port becomes busy after another program starts. Open the site detail page and change the port under **Network**, then start the site again.

<a name="q49"></a>
**Q49: My screen looks stuck on "Creating site".**  
**A49:**
Site creation can take several minutes the first time, because Docker images must be downloaded. Watch the progress bar and the terminal panel for activity. If you want to stop and start over, click **Cancel** in the modal — the wpstaging engine will roll back the half-created site for you. If the modal does not respond at all, open the Settings page, find **Stuck Processes**, and click **Force-cleanup**, then try again.

<a name="q50"></a>
**Q50: The browser says "Your connection is not private" on a local site.**  
**A50:**
Open the Settings page and click **Install local certificate authority**. Enter your password when asked. Then reload the site in the browser.

<a name="q51"></a>
**Q51: I cannot delete a site. The button does nothing.**  
**A51:**
A previous run may still be holding a lock on the site. Open the Settings page, find **Stuck Processes**, and click **Force-cleanup**. Then try **Delete site** again.

<a name="q52"></a>
**Q52: The app shows "Sudo password required" again and again.**  
**A52:**
The app asks for your administrator password only once. After that, it remembers your password while the app stays open. It asks again if you typed the wrong password, canceled the window, or closed and reopened the app. Make sure your user has administrator rights on the computer, and enter the password carefully when prompted.

<a name="q53"></a>
**Q53: The status bar shows low disk space.**  
**A53:**
Free space on the drive that holds your home folder. To remove old Docker images you no longer need, open a terminal and run `docker system prune -a`.

<a name="q54"></a>
**Q54: The app shows the wrong WordPress versions.**  
**A54:**
The list refreshes from the internet every six hours. If you are offline, the app uses the cached list. Open and close the **Create site** window once you are online again to refresh.

---

## More Help

- **[wp-staging.com](https://wp-staging.com)** -- Prices, plans, and product information.
- **[wp-staging.com/support](https://wp-staging.com/support)** -- Get help from our support team.

---

**Last Updated:** 2026-06-26 16:58:41 UTC
