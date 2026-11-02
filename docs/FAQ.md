# WP Staging Desktop FAQ

## General Questions

<a name="q1"></a>
**Q1: What is WP Staging Desktop?**  
**A1:**
WP Staging Desktop is a desktop app for Windows, macOS, and Linux. It lets you create and manage local WordPress sites on your own computer with a few clicks.

<a name="q2"></a>
**Q2: Which operating systems are supported?**  
**A2:**
macOS 13 (Ventura) or newer, Windows 10 or newer, and 64-bit Linux (Ubuntu 20.04+, Debian 11+, Fedora 32+, RHEL 9+). Older systems are not supported.

Version 1.7.1 is the last version that supports macOS 11 (Big Sur) and macOS 12 (Monterey). You can download it from the [1.7.1 release page](https://github.com/wp-staging/wp-staging-desktop/releases/tag/v1.7.1).

<a name="q3"></a>
**Q3: Do I need a license to use this app?**  
**A3:**
No. The app is free for local development. Without a license, you can create local sites and restore a site from a local `.wpstg` backup file.

A WP Staging Developer or Agency license unlocks the Pro features: copy your live site into the app with Remote Sync, restore directly from a backup URL, WP Staging Pro in your local sites, and WP Staging CLI. You can buy a license at [wp-staging.com](https://wp-staging.com).

<a name="q4"></a>
**Q4: Is the app free?**  
**A4:**
Yes. The app is free to download and free for local development. Only the Pro features need a Developer or Agency license. See [Q3](#q3).

<a name="q5"></a>
**Q5: Does this replace the WP Staging WordPress plugin?**  
**A5:**
No. The plugin runs inside your live WordPress site. WP Staging Desktop runs on your own computer to create local test sites. The two work together but solve different problems.

<a name="q5a"></a>
**Q5a: What is the WP Staging Engine?**  
**A5a:**
The WP Staging Engine is the [WP Staging CLI](https://github.com/wp-staging/wp-staging-cli-release), scoped and enhanced to power WP Staging Desktop. It does the heavy lifting for your local sites — creating sites, starting and stopping containers, issuing auto-login URLs, and more. You do not run it yourself; the app drives it behind the scenes. When an engine update is out, the app shows it in the notifications panel, and you click **Update** to install it. The app updates the engine by itself only when your copy is too old to work with the app. The binary file is named `wpstaging`, so in technical messages you may see it called the "wpstaging engine".

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
- Linux: the `.AppImage` is a portable app. Mark it as executable (`chmod +x wpstaging-desktop-*-linux-x64.AppImage`), then double-click to start.

<a name="q8a"></a>
**Q8a: What happens the first time I launch the app?**  
**A8a:**
The app shows a one-time onboarding screen. It downloads the wpstaging engine from the official release and saves it to your user folder. The screen shows a progress bar and confirms the file with a SHA-256 check before saving it.

The file is saved under your own user folder, so no administrator password is needed:

- macOS / Linux: `~/.local/bin/wpstaging`
- Windows: `%LOCALAPPDATA%\Programs\wpstaging\wpstaging.exe`

After this one-time step, the main app opens. If `wpstaging` is already on your computer, the app uses your existing copy and skips this step. If that copy is older than v1.16.0, the app replaces it with a new version in the same place. If the copy is in a system folder, the app asks for your administrator password.

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
SmartScreen warns about new apps until they build up a reputation with Microsoft. This is normal and the warning will stop over time. To continue, click **More info**, then **Run anyway**.

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
The Docker badge at the top of the app shows the Docker state. When Docker is ready, the badge is green and says **Running**.

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
Click the **Add Site** button. Enter a name, pick a PHP and WordPress version, and click **Create Site**. The app downloads the needed images the first time, then sets up the site for you.

<a name="q21a"></a>
**Q21a: How do I change the PHP or WordPress version for an existing site?**  
**A21a:**
Open the site detail page and go to the **PHP & WordPress** tab. Pick a new version from **Switch PHP version** or **Switch WordPress version**, click **Switch**, and confirm the change. The site must be running.

- Switching PHP restarts only this site's containers. The site is offline for a few seconds. Other sites are not affected.
- Switching WordPress replaces the core files in place. The database, plugins, themes, and uploads are preserved. Containers do not restart.

<a name="q21b"></a>
**Q21b: How do I open a command line inside a site?**  
**A21b:**
Open the site detail page, go to the **PHP & WordPress** tab (called **PHP** on a plain PHP site), click **Open Shell**, and confirm. Your terminal application opens with a shell inside the site's PHP container, where the WordPress files are. Use it to run WP-CLI, read files, or check a problem. The site must be running.

If the app cannot open a terminal, it prints the command in the terminal panel at the bottom of the window. Copy that command and run it yourself.

<a name="q21c"></a>
**Q21c: Can a site run on Apache instead of NGINX?**  
**A21c:**
Yes. When you create a site, go to the **Will be created with** row and set **Web server** to **Apache**. To move an existing site, open the site detail page and go to the **PHP & WordPress** tab (called **PHP** on a plain PHP site). Pick a web server from **Switch web server**, click **Switch**, and confirm. The site must be running.

- The Sites list and the site detail page show which web server each site uses.
- Apache needs wpstaging engine v1.16.0 or newer. The app updates an older engine when it starts.
- The first time you use Apache, the app downloads the Apache image. This takes a little longer.
- Switching restarts only this site's containers. The site is offline for a few seconds. Other sites are not affected.
- On Apache, the app updates the WordPress rules in the `.htaccess` file in the site's `www` folder. Lines that Apache cannot use become comments, and a copy of the original file is saved next to it as `.htaccess.wpstg-backup`. The app lists these changes as warnings.
- When you restore a backup to an Apache site, the app warns you about `.htaccess` lines that name the live site's domain. These lines can send visitors to the live site.
- NGINX does not read `.htaccess`. If you move a site back to NGINX, rules you added there no longer apply.

<a name="q21d"></a>
**Q21d: Can a site use MySQL or another MariaDB version?**  
**A21d:**
Yes. When you create a site, go to the **Will be created with** row and set **Database** to the server you want. The choices are MariaDB 11.8, 11.4 and 10.11, and MySQL 8.4 and 5.7. MariaDB 11.8 is the default.

- To change the server of an existing site, open the site detail page. On the **Overview** tab, click **Reset**, and pick a server under **Database server**. Only a reset can change it.
- A reset with a new server clears the site database. To keep the content, restore a backup during the reset.
- The Sites list and the site detail page show which server each site uses.
- A MySQL site still keeps its database files in the `data/mariadb` folder. See [Q22](#q22).
- MySQL 5.7 has no ARM build. It runs slower on Apple Silicon, and it may not start on Windows on ARM.
- A backup from MariaDB 10.10 or newer can fail to restore into a MySQL site with `Unknown collation`. This affects tables that a plugin created without a collation. Keep such a site on MariaDB.
- This needs wpstaging engine v1.16.0 or newer. The app updates an older engine when it starts.

<a name="q21e"></a>
**Q21e: Can I create a site without WordPress, for my own PHP app?**  
**A21e:**
Yes. Click **Add Site** and pick **Plain PHP site**. Enter a name and click **Create Site**. The site gets the same PHP, web server, database, Mailpit, Adminer and HTTPS setup as a WordPress site. The database is empty, and the site's `www` folder holds one placeholder `index.php`. Replace it with your own files.

Your PHP code can read the database settings with `getenv()`: `DB_HOST`, `DB_NAME`, `DB_USER` and `DB_PASSWORD`. Inside the site, `DB_HOST` is `localhost`. The **Database** tab on the site detail page shows the settings for a connection from your computer.

- The Sites list and the site detail page show the site with the label **PHP Site**.
- WordPress actions are hidden for this site: wp-admin, auto-login, the WordPress version switcher, and Pull from production.
- **Reset** deletes all files in the site folder and empties the database. Back up your files first. A reset cannot restore a backup on this site.
- If creating the site fails part-way, the site cannot be created again with the same name. Open it from the Sites list, then reset or delete it.
- This needs wpstaging engine v1.17.0 or newer. With an older engine, the **Plain PHP site** option does not show.
- This needs a paid license. On the free tier, the **Plain PHP site** option shows a **Pro** badge and an upgrade panel.

<a name="q22"></a>
**Q22: Where are my sites stored?**  
**A22:**
In your home folder, under `~/wpstaging/sites/<site-name>/`. Each site keeps its own database files in its `data/mariadb` folder, unless you chose to store the database in a Docker volume.

<a name="q22a"></a>
**Q22a: Should I store the database in a Docker volume?**  
**A22a:**
When you create a site, open **Advanced options** and you will find **Store the database in a Docker volume**. On macOS and Linux it is off by default, so the database files stay in the site folder, where you can open them.

Switch it on to keep them inside Docker instead. This is faster on Docker Desktop, because Docker no longer shares those files with your computer. The downside is that you can no longer open them yourself.

You choose this once, when the site is created, and it cannot be changed later. On Windows the switch is always on and cannot be changed, because Docker always needs a volume there. Deleting the site removes the volume too.

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
On the site detail page, scroll to the **Danger Zone** at the bottom and click **Delete Site**. To confirm, type `delete` in the window that opens. This removes the site files and its database.

<a name="q27"></a>
**Q27: My site shows an HTTPS warning in the browser. How do I fix it?**  
**A27:**
Open the **Settings** page in the app and click **Install local CA**. Enter your password when asked. The next time you open the site, the warning is gone.

<a name="q27a"></a>
**Q27a: Only one of my sites has a certificate warning. How do I fix just that site?**  

**A27a:**
Open the site, then click the **Diagnose & Logs** tab. Find the **Site Certificate** row. If it shows expired, stale, or not trusted, click **Reinstall Certificate** under the **Suggested fix** box. The app reissues this site's certificate and restarts its containers. Other sites and the local certificate authority are not changed.

<a name="q28"></a>
**Q28: What is the terminal panel at the bottom of the app?**  
**A28:**
It shows what the underlying tool is doing. You can copy the text or hide the panel. Power users can read the panel to see the exact commands the app runs.

<a name="q28a"></a>
**Q28a: Can I see the log after my site finishes creating?**  
**A28a:**
Yes. Open the site detail page and click the **Diagnose & Logs** tab. Under **Install Log**, click **Show log** to see the same output the terminal panel showed while the site was created, plus any resets since. Click **Copy** to copy the text. The install log is kept for support and cannot be deleted here; it is removed only when you delete the site.

<a name="q28b"></a>
**Q28b: My site creation failed. How do I send the log to support?**  
**A28b:**
On the failed screen, click **Report a problem**. This opens the feedback form with **Attach site install log** already turned on. You can also click the Help icon in the header at any time, choose **Report a Bug**, and pick the affected site. **Attach site install log** turns on when you pick a site.

<a name="q28c"></a>
**Q28c: Can I see the app's own log?**  
**A28c:**
Yes. Open any site detail page and click the **Diagnose & Logs** tab. Under **Application Log**, click **Show log** to see the app's recent activity. Click **Copy** to copy the text, **Reset** to clear the log (you are asked to confirm first), or **Open logs folder** to find the log files on disk. If a site creation or reset fails, its log is also saved here, so you can still see it even when the site was not created.

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
Yes. Click **Add Site**, choose **Restore from backup**, then pick your `.wpstg` file with **Browse**. You can also paste its path or web address into the **Backup Source** field. The new site is built from your backup.

<a name="q31a"></a>
**Q31a: Where do restored backups go on my computer?**  
**A31a:**
The app keeps extracted and downloaded backups under a folder called **wpstaging-desktop-archive** in your home directory. To change the location, open the **Settings** page and edit **Backup Workspace**. The app creates `wpstaging-output` and `wpstaging-download` subfolders inside your chosen folder.

<a name="q31b"></a>
**Q31b: I restored from a backup URL, but the app used an old copy of the file. How do I get the newest one?**  
**A31b:**
When you restore from a web address, the app reuses the file it already downloaded, so a second restore is much faster. If the file on the server has changed, switch on **Download again** under the backup field. The app then downloads the file again and replaces the old copy. The switch only appears when there is an old copy to reuse, so you will not see it for a file on your computer or for a web address you have never downloaded from. The small information icon next to the switch explains what it does.

<a name="q31c"></a>
**Q31c: Why does the app warn that a port is already in use?**  
**A31c:**
Another program on your computer is already using port 80 or 443 for every address. Web servers, some virtual machine tools, and other local development apps do this. The site is still created, but it runs on a different port, so its address includes that port number, for example `https://my-site.local:4444`.

You have two choices. Click **Create Anyway** to accept the different port. Or click **Cancel**, close the other program, and create the site again to get the standard port.

To see the current answer at any time, open the site detail page, click the **Diagnose & Logs** tab, and look at the **Port Availability** row.

<a name="q31d"></a>
**Q31d: After a restore, some URLs still use another host, such as my CDN. How do I change them?**  
**A31d:**
A restore changes only the site's own hosts: the site address, the home address, and each subsite of a network. All other hosts keep their URLs. For example, if your site is `example.com`, the URLs of `cdn.example.com` and `www.example.com` stay as they are.

To change this, use the **URLs** section in **Add Site** or **Reset Site**. It stays hidden until you choose a backup:

1. In **Add Site**, choose **Restore from backup** and pick your `.wpstg` file. In **Reset Site**, pick your `.wpstg` file in **Backup file (optional)**.
2. Click **URLs** under the backup field to open the section.
3. Click **Add host** or **Add URL** to add a row.

The section has two lists:

- **Replace host** moves the URLs of one host to a new host, for example `media.example.com` to `media.example.local`. Each URL keeps its `http` or `https`. Only that exact host changes, not the hosts under it.
- **Keep URL** leaves every URL that starts with a value unchanged, for example `https://example.com/wp-content/uploads`. The same URL with the other scheme or without a scheme also stays. If the value names your site's own host, add a path.

Keep these points in mind:

- Only URLs in the database change. The new host must still work on your computer.
- **Replace host** cannot change the site's own host or a subsite host. The app cannot check this before the restore starts, so the error appears in the log during the restore. On **Reset Site**, the site is already empty at that point.
- The section needs wpstaging engine v1.18.0 or newer. With an older engine, it does not show. It also does not show for a backup web address without a license.

<a name="q31e"></a>
**Q31e: How do I export a site as a static website?**  
**A31e:**
Open the site detail page. On the **Overview** tab, find **Export static website** above **Reset Site** and click **Export**. The site must be running. Click **Export** again in the window that opens. The export holds the HTML, CSS, JavaScript and media files of the site. Any web host can serve these files without PHP or a database.

The form has these optional fields:

- **Output folder:** where the files go. If you leave it empty, the app uses the `static` folder in the site folder.
- **Base URL:** the address the static website will have. If you leave it empty, the export uses relative links.
- **Exclude:** skips the URLs that match a pattern, such as `/shop/` or `*.zip`.
- **Include:** also saves a URL or path that no link reaches.

Keep these points in mind:

- Comments, search, forms and login do not work in a static copy.
- If you choose an output folder that already exists, the app asks first. The export refuses a folder that holds other files, and the error names them.
- A failed home page stops the export. Other failed URLs are listed when the export ends.
- If you cancel, the app removes the partial export. An earlier export stays as it was.
- For a multisite, only the site's own hostname is exported. A subsite on another hostname is a separate export.
- A site with **Plain** or `index.php` permalinks exports only the home page. Choose another permalink structure in WordPress first.
- While the export runs, the site cannot be stopped, reset or deleted.
- This needs a paid license and wpstaging engine v1.18.0 or newer. With an older engine, the action does not show.

<a name="q32"></a>
**Q32: How do I see all running containers?**  
**A32:**
Open the **Containers** page from the sidebar (or top navigation). It shows every container that belongs to your sites, with its image, status, and ports.

---

## License Questions

<a name="q33"></a>
**Q33: How do I enter my license key?**  
**A33:**
Open the **Pro** page in the menu. It is called **License** after you activate a license. Paste your key and click **Activate License**.

<a name="q34"></a>
**Q34: Does the app work offline?**  
**A34:**
Yes, most of the time. The internet is needed to download the wpstaging engine the first time, to pull Docker images, and to check a paid license. The free tier needs no internet for its license check.

With a paid license, the wpstaging engine checks the license online and keeps the result for 4 hours. After that, it needs the internet again the next time you create, start, or change a site.

<a name="q35"></a>
**Q35: How long is my license remembered?**  
**A35:**
The wpstaging engine checks your license online and keeps the result for 4 hours. After that, it checks again the next time you create, start, or change a site. **Check Status** on the License page shows the saved license details. It does not start a new online check.

<a name="q36"></a>
**Q36: I see "Invalid license key" but I have a valid key.**  
**A36:**
Check your internet connection. Then paste your key again on the License page and click **Activate License**. If the problem stays, contact [WP Staging support](https://wp-staging.com/support).

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
From version 1.3.0 the app updates itself. When a new version is ready, the bell at the top shows a **Desktop App Update** card. Click **Download**, wait for the progress bar, then click **Restart & Install**. The app closes, installs the update, and opens again. Nothing is downloaded or installed without your click.

You still need to update by hand in two cases:

- **You use version 1.2.2 or older.** These versions cannot update themselves. Install version 1.3.0 by hand one time. After that the app takes over.
- **You use the Windows portable build.** It has no installer, so it cannot update itself.

On macOS 11 (Big Sur) and macOS 12 (Monterey), the app does not offer versions after 1.7.1. These versions need macOS 13 or newer. See [Q2](#q2).

To update by hand, open the [WP Staging Desktop releases page](https://github.com/wp-staging/wp-staging-desktop/releases), download the new file for your system, and then:

- macOS: open the new `.dmg` and drag the app to Applications. Choose **Replace** when asked.
- Windows: run the new installer. It will close the old app and update it for you.
- Linux: replace your old `.AppImage` with the new one. Mark the new file as executable.

Your sites are kept.

Settings has a **Receive beta updates** toggle. It is off by default, so you only get stable versions. Turn it on if you want to test new versions early.

<a name="q39a"></a>
**Q39a: What are the notifications shown by the bell icon?**  

**A39a:**
The bell at the top of the app shows three kinds of messages:

- An available **Desktop App Update**, with a Download button.
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
- Remove unused Docker images by opening a terminal and running `docker system prune -a`. This removes every image that no running site uses, so Docker downloads them again the next time a stopped site starts. It also removes all stopped containers, unused networks, and build cache, including ones that other programs use.

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

- **wp-staging.com** to check a paid license, to load announcements shown in the app, to report that the wpstaging engine was installed or updated, and to send a Help & Feedback message when you submit one.
- **GitHub** to download the wpstaging engine, to check for a new wpstaging engine version (at most once a day), and to check for a new app version (every 4 hours).
- **Docker Hub** to download container images the first time.
- **api.wordpress.org** to get the list of recent WordPress versions.


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
**Q46: The Docker badge says Docker is not running.**  
**A46:**
Open Docker Desktop (or your Docker tool) and wait until it shows it is ready. The badge in the app updates by itself.

<a name="q47"></a>
**Q47: A site will not start.**  
**A47:**
First check the Docker badge. If Docker is running, open the terminal panel at the bottom and click **Start** again. The error in the panel often tells you what is wrong (a missing tool, a port already in use, or an old container).

<a name="q48"></a>
**Q48: Two sites try to use the same port.**  
**A48:**
The app picks a free port for each new site, but sometimes a port becomes busy after another program starts. Open the site detail page and change the port under **Network**, then start the site again. Changing a port needs wpstaging engine v1.16.1 or newer.

<a name="q49"></a>
**Q49: My screen looks stuck on "Creating site".**  
**A49:**
Site creation can take several minutes the first time, because Docker images must be downloaded. Watch the progress bar and the terminal panel for activity. If you want to stop and start over, click **Cancel** in the modal — the wpstaging engine will roll back the half-created site for you. If the modal does not respond at all, open the Settings page, find **Stuck Processes**, and click **Force-cleanup**, then try again.

<a name="q50"></a>
**Q50: The browser says "Your connection is not private" on a local site.**  
**A50:**
Open the Settings page and click **Install local CA**. Enter your password when asked. Then reload the site in the browser.

<a name="q51"></a>
**Q51: I cannot delete a site. The button does nothing.**  
**A51:**
A previous run may still be holding a lock on the site. Open the Settings page, find **Stuck Processes**, and click **Force-cleanup**. Then try **Delete Site** again.

<a name="q52"></a>
**Q52: The app shows "Sudo password required" again and again.**  
**A52:**
The app asks for your administrator password only once. After that, it remembers your password for up to 12 hours while the app stays open. It asks again if you typed the wrong password, canceled the window, or closed and reopened the app. Make sure your user has administrator rights on the computer, and enter the password carefully when prompted.

<a name="q53"></a>
**Q53: My disk is almost full.**  
**A53:**
The status bar at the bottom shows how much disk space is used. Free space on the drive that holds your home folder. See [Q41](#q41) for how to remove sites and old Docker images.

<a name="q54"></a>
**Q54: The app shows the wrong WordPress versions.**  
**A54:**
The app refreshes the list from the internet when it starts and every six hours while it runs. If you are offline, the app uses the last saved list. It gets the new list at the next refresh after you are online again.

---

## More Help

- **[wp-staging.com](https://wp-staging.com)** -- Prices, plans, and product information.
- **[wp-staging.com/support](https://wp-staging.com/support)** -- Get help from our support team.

---

**Last Updated:** 2026-10-30 15:03:43 UTC
