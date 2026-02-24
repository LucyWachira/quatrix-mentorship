
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
  1. Do a proper backup (in depth)
  2. Fully update Bookworm
  3. Change repositories to Trixie
  4. Perform the upgrade safely - then Verify Debian 13

- sudo systemctl stop traccar
1. Backup 
- Create a Backup Directory - mkdir -p /backup → creates the /backup folder if it doesn’t exist and keeps all backups organized in one place, prevents clutter in /. `sudo mkdir -p /backup`

2. Backup System Configurations and User Data
`sudo tar -cvpzf /backup/system-backup-bookworm.tar.gz /etc /home`
  - /etc → all system configuration files (network, services, Traccar, PostgreSQL config, etc.)
  - /home → all user files (important if multiple users have files on the server)
  - Verify backup: `ls -lh /backup`

3. Backup PostgreSQL Databases
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
4. Backup APT Sources: `sudo cp -r /etc/apt /backup/apt-config-backup`
- This saves your package manager configuration. If something breaks during repo updates, you can restore it.

5. Update Package Lists: `sudo apt update` Updates the list of available packages and their versions from current repositories.  you can do a minimal upgrade: sudo apt upgrade before doing a full-upgrade.
6. Full upgrade: `sudo apt full-upgrade ` Upgrades all installed packages to their latest versions
7. Remove Unnecessary Packages: `sudo apt autoremove`
8. Reboot System: `sudo reboot`
9. SWITCH TO TRIXIE REPOSITORIES
  - Edit Sources List:`sudo vi /etc/apt/sources.list`
  - Replace all occurrences of bookworm with trixie.

- FIXING BROKEN PIPE ISSUE:
  - `sudo kill 1588`- Sending a kill signal terminated the hanging apt upgrade process.
  - `sudo apt install -f` - The -f flag stands for “fix-broken”.This command tells apt to repair any dependency issues from partially installed or broken packages. If a previous upgrade was interrupted (like the broken pipe), this step ensures all packages are in a consistent state.
  - `sudo apt full-upgrade` -full-upgrade will upgrade packages and install or remove packages as needed to satisfy dependencies.This ensures your system is fully up-to-date and no half-installed packages remain.
  - To check for broken packages - `sudo dpkg --audit` - This lists any packages that are only partially installed or in an inconsistent state, Ideally it should return nothing
  **5. Update the hostname so that it reads test-traccar**
  - `hostname` - To check the current hostname.
  - `sudo hostnamectl set-hostname test-traccar` - To update the hostname permanently.
  - `sudo nano /etc/hosts` - Open the file, find the line that looks like:  127.0.1.1 old-hostname and change it to: 127.0.1.1 test-traccar
  - you can do a sudo reboot:
  - verify the change: `hostname` should now read test-traccar
