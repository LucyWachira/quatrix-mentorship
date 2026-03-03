
## Practical Assessment #1 - Test Traccar

### Basic Linux Administration

**1. Access:**
  - ssh into the server to ensure you have access.

  `ssh lwachira@test.traccar.quatrixglobal.com`

  - Add an ssh key for your account that you will use to access the server using juice-ssh or a different mobile ssh client of your choice. This is just in case your IP is blocked by fail2ban, you can use your phone to log in and unban the IP.
   - I downloaded Termius on  my phone and generated an ssh key: `ecdsa-sha2-nistp521 AAAAE2VjZHNhLXNoYTItbmlzdHA1MjEAAAAIbmlzdHA1MjEAAACFBAD3Tey80bgv4fgzgevXI3bbSU7WstACViYB5QpA4XHPNsBikfbT0LVecswWRcKnOBdbi2CinvsHF0dHoIEmQPuzwgFKpFRSGfbKiacH/9mnQDsCuyw7WazoeY4ZhrC5mBbBEFPPOAg6eQVV6qKCreyb+SoAkmlPZWBjwV/PaSweWmK8Bg==`
   - I then added the key to my authorised keys:
   ```
   lwachira@test:~$ cat ~/.ssh/authorized_keys 
    ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBLX3U7/q8c5tndDHLPoQ4t8HNkUWwWSDxlrkE2in+ZcCbNaH7utWLn3k4kTsmIwI73yvfJ8XAwOX/GsTBR6FCFA= lwachira@gndungu

   ## Termius
    ecdsa-sha2-nistp521 AAAAE2VjZHNhLXNoYTItbmlzdHA1MjEAAAAIbmlzdHA1MjEAAACFBAD3Tey80bgv4fgzgevXI3bbSU7WstACViYB5QpA4XHPNsBikfbT0LVecswWRcKnOBdbi2CinvsHF0dHoIEmQPuzwgFKpFRSGfbKiacH/9mnQDsCuyw7WazoeY4ZhrC5mBbBEFPPOAg6eQVV6qKCreyb+SoAkmlPZWBjwV/PaSweWmK8Bg==
   ```
  - Now I am able to ssh to test traccar via my phone on termius.
**2. Check the current version of:**
  - Linux - `uname -r
              6.1.0-31-amd64`

  - Debian- 
 ```
  cat /etc/os-release 
  PRETTY_NAME="Debian GNU/Linux 12 (bookworm)"
  NAME="Debian GNU/Linux"
  VERSION_ID="12"
  VERSION="12 (bookworm)"
  VERSION_CODENAME=bookworm
  ID=debian
  HOME_URL="https://www.debian.org/"
  SUPPORT_URL="https://www.debian.org/support"
  BUG_REPORT_URL="https://bugs.debian.org/"
```
**3. Run updates on the system. Update Debian to version 13.0 (Trixie).**
- Update the apt repositories and then fully upgrade the test.traccar Debian Linux.
  - I am currently on:Debian 12 (Bookworm) Kernel: 6.1
  - Now I will:
  1. Do a proper backup 
  2. Fully update Bookworm
  3. Change repositories to Trixie
  4. Perform the upgrade safely - then Verify Debian 13

**1. Backup**
- Create a Backup Directory - mkdir -p /backup → creates the /backup folder if it doesn’t exist and keeps all backups organized in one place, prevents clutter in /. `sudo mkdir -p /backup`
- Backup System Configurations and User Data
`sudo tar -cvpzf /backup/system-backup-bookworm.tar.gz /etc /home`
  - /etc → all system configuration files (network, services, Traccar, PostgreSQL config, etc.)
  - /home → all user files (important if multiple users have files on the server)
  - Verify backup: `ls -lh /backup`

- Backup PostgreSQL Databases
`sudo -u postgres pg_dumpall > /backup/postgres-all-databases.sql`

```
 sudo -u postgres pg_dumpall > /tmp/postgres-all.sql
 sudo mv /tmp/postgres-all.sql /backup/
 ls -lh /backup
 sudo gzip /backup/postgres-all.sql
```

- Backup of Logs:
```
 sudo tar -cvpzf /backup/logs-backup.tar.gz /var/log
```
- This includes:
  - System logs
  - Boot logs
  - Error logs
  - Service logs
  - Authentication logs
  - Package installation logs
- Backup APT Sources: `sudo cp -r /etc/apt /backup/apt-config-backup`
- This saves your package manager configuration. If something breaks during repo updates, you can restore it.

**2. Update Package Lists:** `sudo apt update` Updates the list of available packages and their versions from current repositories.  you can do a minimal upgrade: sudo apt upgrade before doing a full-upgrade.

**3. Full upgrade:** `sudo apt full-upgrade ` Upgrades all installed packages to their latest versions

**4. Remove Unnecessary Packages:** `sudo apt autoremove`

**5. Reboot System:** `sudo reboot`

**6. SWITCH TO TRIXIE REPOSITORIES**
  - Edit Sources List:`sudo vi /etc/apt/sources.list`
  - Replace all occurrences of bookworm with trixie.

**- FIXING BROKEN PIPE ISSUE:**
  - `sudo kill 1588`- Sending a kill signal terminated the hanging apt upgrade process.
  - `sudo apt install -f` - The -f flag stands for “fix-broken”.This command tells apt to repair any dependency issues from partially installed or broken packages. If a previous upgrade was interrupted (like the broken pipe), this step ensures all packages are in a consistent state.
  - `sudo apt full-upgrade` -full-upgrade will upgrade packages and install or remove packages as needed to satisfy dependencies.This ensures your system is fully up-to-date and no half-installed packages remain.
  - To check for broken packages - `sudo dpkg --audit` - This lists any packages that are only partially installed or in an inconsistent state, Ideally it should return nothing.

  **5. Update the hostname so that it reads test-traccar**
  - `hostname` - To check the current hostname.
  - `sudo hostnamectl set-hostname test-traccar` - To update the hostname permanently.
  - `sudo vi /etc/hosts` - Open the file, find the line that looks like:  127.0.1.1 old-hostname and change it to: 127.0.1.1 test-traccar
  - you can do a sudo reboot:
  - verify the change: `hostname` should now read test-traccar

**3. Fail2ban updating:**
- Check the nginx logs for potential intrusion attacks Usually requests that end in 404 are potential attacks
  - I am to review the Nginx logs to identify possible intrusion attempts. Locate the logs : `ls /var/log/nginx`
  - `sudo cat /var/log/nginx/access.log` - contains a record of eveyone who has tried to access the server through Nginx.
  - `sudo grep "404" /var/log/nginx/access.log` -to get requests that end in 404.

  - To edit the nginx brute file: `sudo vi /etc/fail2ban/filter.d/nginx-brute.conf `

  - This is now the complete regex:
```
  sudo cat /etc/fail2ban/filter.d/nginx-brute.conf 
[Definition]

failregex = ^<HOST> .* "(GET|POST).*\.env.*"
            ^<HOST> .* "(GET|POST).*\.git.*"
            ^<HOST> .* "(GET|POST).*\.aws.*"
            ^<HOST> .* "(GET|POST).*credentials.*"
            ^<HOST> .* "(GET|POST).*geoserver.*"
            ^<HOST> .* "(GET|POST).*owa.*"
            ^<HOST> .* "(GET|POST).*_profiler.*"
            ^<HOST> .* "(GET|POST).*load.js.*"
            ^<HOST> .* "(GET|POST).*var/task.*"
            ^<HOST> .* "(GET|POST).*error/.*"
            ^<HOST> .* "(GET|POST).*\.\..*"
            ^<HOST> .* "(GET|POST).*config.*"
            ^<HOST> .* "(GET|POST).*serverless.*"
            ^<HOST> .* "(GET|POST).*package.json.*"
            ^<HOST> .* "(GET|POST).*vercel.*"
            ^<HOST> .* "(GET|POST).*mcp.*"
            ^<HOST> .* "(GET|POST).*sse.*"
            ^<HOST> .* "(GET|POST).*info.php.*"
            ^<HOST> .* "(GET|POST).*Dr0v.*"
            ^<HOST> .* "(GET|POST).*database.*"
            ^<HOST> .* "(GET|POST).*yml.*"
            ^<HOST> .* "(GET|POST).*ab2g.*"

ignoreregex =
```

-  Then restart fail2ban:
`sudo systemctl restart fail2ban.service`

- To check the jail: ` sudo cat /etc/fail2ban/jail.local `
- To verify if the filter is working :
`sudo fail2ban-regex /var/log/nginx/access.log /etc/fail2ban/filter.d/nginx-brute.conf`

**- Exempt Applewood, Trio, and the Yard offices from the sshd and nginx-brute filters.**

- ` sudo vi /etc/fail2ban/jail.local ` to edit the file then add ignore ip:
```
[nginx-brute]
enabled  = true
port     = http,https
filter   = nginx-brute
logpath  = /var/log/nginx/access.log
bantime = 96h
maxretry = 2
findtime = 24h

ignoreip = 197.232.110.49  102.215.13.101  41.90.170
```


4. Create user accounts for your fellow interns - They should all be able to log in (only using ssh keys as the authentication mode) and verify sudo authorization. Format for usernames should be e.g. for Jane Doe, her username should be jdoe
Ensure that users can only ssh to the server using ssh key (ie they should not be prompted for a password when first logging in to the server. The password is only to be invoked when running sudo based commands).
Every user should also be able to ssh to the server via juice-ssh.
The several public ssh-keys listed in the appropriate file on the server should be aptly labeled so that one can differentiate between them in case a user has several devices that they will access the server from. In our case, every user should have at least 2 devices that they can access the server:
The PC - work or personal
Their Phone (using juice-ssh or connect-bot apps)
Hint: There’s a safe way to label keys without damaging the actual key.

- I created gwekesa on my local pc :ls /home - I should see all users. I navigated to user gwekesa : `su - gwekesa` I generated her ssh keys: `ssh-keygen -t ecdsa`. Then `cat ~/.ssh/id_ecdsa.pub` to view her public key.
  - I navigated to test traccar: `ssh lwachira@test.traccar.quatrixglobal.com` then switched to user gwekesa `su - gwekesa` that i created :`sudo adduser gwekesa` `sudo usermod-aG sudo gwekesa`.
  - Created the ssh directory `mkdir -p ~/.ssh`
  - Created the authorized_keys file :` touch authorized_keys` or you can create it and edit it directly using: `sudo vi authorized_keys`
  - You can now paste the keys under the authorized keys
  - Her Traccar passwd: wekesa1234, local gwekesa user on my pc passwd: Gwekesa



### Test Traccar - Upgrade & Configuration

- Update test traccar to the version 6.9.1. Keenly read the release notes as sometimes Traccar changes major items when a new version comes through. The default URL points to the modern UI. However, we still provide the Legacy UI for stubborn users who have refused to switch over to the modern UI that is now the default and ONLY UI supported by Traccar developers.
- changes:
  - Trip processing changes are the biggest functional change → check trip reports after upgrade.
  - Modern UI is now default and only officially supported → always backup legacy folder before upgrading.
  - Reporting & notifications have several new features → check geofence reports, timelines, and WhatsApp notifications.
  - Security & stability → multiple fixes and session security improvements.
  - Device support & backend changes → new devices and protocol (Smartcar), minor fixes, database retention changes.

**1. Prior to starting the process, make sure to:
Study and the existing traccar nginx configurations to understand how the reverse proxy works. Note down different components of custom nginx configuration files specifically used for `Test Traccar Web Applications.**

- Locate the Nginx Configuration Files: are in `/etc/nginx/sites-available/`: 
  - test.traccar.quatrixglobal.com.conf         # Modern UI
  - legacy.test.traccar.quatrixglobal.com.conf  # Legacy UI
  - These files tell Nginx how to handle incoming web requests for each URL. Nginx acts as a traffic director: it decides whether a user sees the Modern UI, the Legacy UI, or nothing.

  - `sudo cat /etc/nginx/sites-available/test.traccar.quatrixglobal.com.conf`

  ```
  server {
	#listen 80;
        listen 443 ssl http2;
        listen [::]:443 ssl http2;

	server_name test.traccar.quatrixglobal.com;
	root /opt/traccar/modern;

	ssl_certificate /etc/letsencrypt/live/test.traccar.quatrixglobal.com/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/test.traccar.quatrixglobal.com/privkey.pem;
        include /etc/letsencrypt/options-ssl-nginx.conf;
        ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem;

	location / {
		proxy_pass http://127.0.0.1:8082;
		proxy_http_version 1.1;
		proxy_set_header Upgrade $http_upgrade;
		proxy_set_header Connection "upgrade";
		proxy_cookie_path / "/; secure; HttpOnly; SameSite=None";
	}

	location /api/socket {
		proxy_pass http://localhost:8082/api/socket;
		proxy_http_version 1.1;
		proxy_set_header Upgrade $http_upgrade;
		proxy_set_header Connection "upgrade";
		proxy_cookie_path / "/; secure; HttpOnly; SameSite=None";
	}
  }
  ```
1. Listening Ports : `listen 443 ssl http2;
listen [::]:443 ssl http2;`
  - What it does: Nginx is listening on HTTPS port 443, both for IPv4 and IPv6.Users access the site via https://test.traccar.quatrixglobal.com.Don’t change this; the new Traccar version still serves the web UI on a port like 8082.
2. Server Name: `server_name test.traccar.quatrixglobal.com;`
  - What it does: This config applies to requests for test.traccar.quatrixglobal.com.
3. Root Directory: `root /opt/traccar/modern;`This is where the Modern UI files live. (Mostly for serving static content.)
4. SSL Certificates:
```
ssl_certificate /etc/letsencrypt/live/test.traccar.quatrixglobal.com/fullchain.pem;
ssl_certificate_key /etc/letsencrypt/live/test.traccar.quatrixglobal.com/privkey.pem;
include /etc/letsencrypt/options-ssl-nginx.conf;
ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem;
```
  - What it does: Enables HTTPS using Let’s Encrypt certificates.Encrypts traffic between users and server.During Upgrade ,Keep these paths intact; do not overwrite.
5. Main Location (/) → Modern UI
  ```location / {
    proxy_pass http://127.0.0.1:8082;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection "upgrade";
    proxy_cookie_path / "/; secure; HttpOnly; SameSite=None";
  }
  ```
  - What it does: For all normal requests (/), Nginx forwards traffic to Traccar running on localhost:8082.
  - proxy_set_header Upgrade and Connection "upgrade" → supports WebSocket connections.
  - proxy_cookie_path → ensures cookies work securely over HTTPS.

- A **reverse proxy** is like a middleman or traffic controller between users and a server.
  - Users don’t connect to the server directly.
  - They connect to the reverse proxy first (Nginx in our case).
  - The reverse proxy forwards the request to the server (Traccar) and then sends the response back to the user.


- Note the traccar configuration files and their contents. Familiarize yourself with the diff command. Always view the differences between 2 similar files before overwriting content from one to the other.

  - File location:`sudo cat /opt/traccar/conf/traccar.xml ` - This file tells Traccar how to run, especially database and map settings.
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE properties SYSTEM 'http://java.sun.com/dtd/properties.dtd'>
<properties>
    
    <!-- Documentation: https://www.traccar.org/configuration-file/ -->

    <!-- Postgres SQL Database -->
    <entry key='database.driver'>org.postgresql.Driver</entry>
    <entry key='database.url'>jdbc:postgresql://127.0.0.1:5432/traccar</entry>
    <entry key='database.user'>traccar</entry>
    <entry key='database.password'>bebavitu</entry>
    <entry key='database.historyDays'>90</entry>

    <!-- LocationIQ details -->
    <entry key='geocoder.enable'>true</entry>
    <entry key='geocoder.type'>nominatim</entry>
    <entry key='geocoder.url'>http://nominatim.quatrixglobal.com/reverse.php</entry>
    <entry key='geocoder.format'>%h, %r, %u, %t, %s, %c</entry>
    
</properties>
```
1. Database Configuration
```
<entry key='database.driver'>org.postgresql.Driver</entry>
<entry key='database.url'>jdbc:postgresql://127.0.0.1:5432/traccar</entry>
<entry key='database.user'>traccar</entry>
<entry key='database.password'>bebavitu</entry>
<entry key='database.historyDays'>90</entry>
```
 - What this does- This tells Traccar:
     - Use PostgreSQL database
    - Database server → 127.0.0.1
    - Port → 5432
    - Database name → traccar
    - Username → traccar
    - Password → bebavitu
    - Keep data for 90 days
 - This is critical - If you lose this:Traccar won't connect to the database, Devices and users disappear, Server won't start properly
    - This must be restored after upgrade
  
2. Geocoder Configuration:
```
<entry key='geocoder.enable'>true</entry>
<entry key='geocoder.type'>nominatim</entry>
<entry key='geocoder.url'>http://nominatim.quatrixglobal.com/reverse.php</entry>
<entry key='geocoder.format'>%h, %r, %u, %t, %s, %c</entry>
```
- What this does:  This converts GPS coordinates to real addresses. Example:Instead of -1.2921, 36.8219 You see : Moi Avenue, Nairobi, Kenya
 - Custom part: You are using a custom geocoder server:`http://nominatim.quatrixglobal.com`
- Why You Must Use diff Before Copying: After installing Traccar 6.12.1 you will get a new traccar.xml. If you overwrite it with the old file: You lose new features, Traccar may break: `diff old-traccar.xml new-traccar.xml`


**2. Backup the legacy folder before uninstallation. The legacy UI was discontinued in the official Traccar updates releases sometime around Traccar 6.0 and therefore anyone that needs legacy UI needs to back it up during upgrades otherwise you lose that feature.**
- File Creation: `sudo vi backup-traccar.sh`
```
#!/bin/bash

DATE=$(date +%F)
BACKUP_DIR="/backup/traccar"

mkdir -p $BACKUP_DIR

echo "Backing up Traccar..."

# Backup traccar.xml
cp /opt/traccar/conf/traccar.xml $BACKUP_DIR/traccar.xml.$DATE

# Backup conf directory
tar -czf $BACKUP_DIR/conf-$DATE.tar.gz /opt/traccar/conf

# Backup legacy folder
tar -czf $BACKUP_DIR/legacy-$DATE.tar.gz /opt/traccar/legacy

echo "Backup completed. Files saved in $BACKUP_DIR"
```

  - DATE=$(date +%F)- Creates a variable called DATE that stores today’s date.
- BACKUP_DIR="/backup/traccar"- Creates a variable BACKUP_DIR that stores the folder where backups will be saved.
- mkdir -p $BACKUP_DIR- Creates the backup folder, -p ensures any parent folders are created too.
- cp /opt/traccar/conf/traccar.xml $BACKUP_DIR/traccar.xml.$DATE - Copies the main Traccar configuration file (traccar.xml) to the backup folder. Adds the date to the filename (traccar.xml.2026-03-02) so it doesn’t overwrite previous backups.
- tar -czf $BACKUP_DIR/conf-$DATE.tar.gz /opt/traccar/conf- Creates a compressed archive of the entire conf folder.


- Make Script Executable: `sudo chmod +x backup-traccar.sh`
- Run the Script: `sudo ./backup-traccar.sh`
  - Copied traccar.xml
  - Compressed /opt/traccar/conf into conf-2026-03-02.tar.gz
  - Compressed /opt/traccar/legacy into legacy-2026-03-02.tar.gz
- Verify the Backup: `ls /backup/traccar/`
  - Configuration file
  - Configuration folder
  - Legacy UI folder


- sudo systemctl stop traccar
- wget https://www.traccar.org/download/traccar-linux-64-latest.zip -O traccar-linux-64-latest.zip
- unzip traccar-linux-64-latest.zip
- sudo sh traccar.run --target /opt/traccar-new
- diff to compare the new and old .xml file- `diff /backup/traccar/traccar.xml.2026-03-02 /opt/traccar/conf/traccar.xml`

- Restore back the legacy file:  `sudo tar -xzvf /backup/traccar/legacy-2026-03-02.tar.gz -C /opt/traccar-new/`
- Start the traccar server.

- Check the logs to ensure there are no issues. Share a command and filter that would help you identify only the WARN - ie WARNING messages in the traccar logs.
  - `sudo tail /opt/traccar-new/logs/tracker-server.log`
  
  - Only filter WARN: `sudo tail /opt/traccar-new/logs/tracker-server.log | grep "WARN"`