
### Practical Assessment #2 - Test Jenkins

#### Basic Linux Administration
1. Update Debian to version 13.0 Trixie
 - First confirm current version:cat /etc/os-release
 ```
cat /etc/os-release 
PRETTY_NAME="Debian GNU/Linux 11 (bullseye)"
NAME="Debian GNU/Linux"
VERSION_ID="11"
VERSION="11 (bullseye)"
VERSION_CODENAME=bullseye
ID=debian
HOME_URL="https://www.debian.org/"
SUPPORT_URL="https://www.debian.org/support"
BUG_REPORT_URL="https://bugs.debian.org/"
```

- Update current packages:
```
sudo apt update
sudo apt upgrade
sudo apt full-upgrade
```

- Edit sources list:`sudo vi /etc/apt/sources.list` Replace current bullseye with bookworm
```
sudo cat /etc/apt/sources.list
deb http://deb.debian.org/debian bookworm main
deb-src http://deb.debian.org/debian bookworm main
deb http://security.debian.org/debian-security bookworm-security main
deb-src http://security.debian.org/debian-security bookworm-security main
deb http://deb.debian.org/debian bookworm-updates main
deb-src http://deb.debian.org/debian bookworm-updates main
deb http://deb.debian.org/debian bookworm-backports main
deb-src http://deb.debian.org/debian bookworm-backports main
```
- Upgrade to Debian 12: 

```
sudo apt update
sudo apt full-upgrade
sudo reboot
```
- After reboot: cat /etc/os-release
```PRETTY_NAME="Debian GNU/Linux 12 (bookworm)"
NAME="Debian GNU/Linux"
VERSION_ID="12"
VERSION="12 (bookworm)"
VERSION_CODENAME=bookworm
ID=debian
HOME_URL="https://www.debian.org/"
SUPPORT_URL="https://www.debian.org/support"
BUG_REPORT_URL="https://bugs.debian.org/"
```
- Repeat that again to upgrade to Trixie.


2. Update the hostname so that it reads test-jenkins and not just test

- Check current hostname:`hostname`
test

- Set new hostname:
`sudo hostnamectl set-hostname test-jenkins`

- Now update hosts file:change test to test-jenkins
`sudo vi /etc/hosts`
verify:
sudo cat /etc/hosts
```
# Your system has configured 'manage_etc_hosts' as True.
# As a result, if you wish for changes to this file to persist
# then you will need to either
# a.) make changes to the master file in /etc/cloud/templates/hosts.debian.tmpl
# b.) change or remove the value of 'manage_etc_hosts' in
#     /etc/cloud/cloud.cfg or cloud-config from user-data
#
127.0.1.1 test.jenkins.quatrixglobal.com test-jenkins
127.0.0.1 localhost

# The following lines are desirable for IPv6 capable hosts
::1 ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
ff02::3 ip6-allhosts
```
- Then `sudo reboot` check th hostname: `hostname` its now: 
test-jenkins

- Create user accounts for the other interns and Kelvin and Tevin. Format for usernames should be e.g. for Jane Doe, her username should be jdoe.
`sudo adduser gwekesa`

- Make all users sudoers.
`sudo usermod -aG sudo gwekesa`

- They should all be able to log in (only using ssh keys as the authentication mode) and verify sudo authorization. Ensure that this is enforced. Test it to verify.
- Every user should also be able to ssh to the server via juice-ssh.
- The several public ssh-keys listed in the appropriate file on the server should be aptly labeled so that one can differentiate between them in case a user has several devices that they will access the server from. In our case, every user should have at least 2 devices that they can access the server:
- The PC - work or personal
- Their Phone (using juice-ssh)
`gwekesa@test-jenkins:~$ sudo cat ~/.ssh/authorized_keys `

```
## PC
ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBCAIhRbWFXIAj12vQ+i8VJB3ljJrT7MJoSfPlRsHo/Ck/qWiAw4WCZH08FHGqVMWISJhB3DPUfOpYRcQCiOi7qA= gwekesa@gwekesa

## Termius
ecdsa-sha2-nistp521 AAAAE2VjZHNhLXNoYTItbmlzdHA1MjEAAAAIbmlzdHA1MjEAAACFBAAl2oxylPk05akl6IIgFUo10904S50n54QKWpDtC1MeVF0LNFkXFBgrQDdKoZ0/MmKLqmynx9ogqUwALo1JnAC3NwFipwBy8Qpq+qXzaXtOQu7bfpHgQy1ikHBYFoYBHuiK7K4Hb2JVmxc/cJvuEquxWqbNgzm0xU3RiPTpJV8GdJvPuQ==
gwekesa@test-jenkins:~$ 
```

### Networking & Security
- Ensure sshd (OpenSSH) on the server is configured such that:
  - Users can only authenticate using an ssh key
  `sudo vi /etc/ssh/sshd_config`
  allowed the `#PubkeyAuthentication yes`
  - The root user is blocked from accessing ssh access remotely.
  `PermitRootLogin no` set the root login to no.

- Install ufw and enable:
    - OpenSSH
   - HTTP
   - HTTPS

- To install `sudo apt update` then `sudo apt install ufw`

```sudo ufw allow openSSH
sudo ufw allow http
sudo ufw allow https
```

  - To check :`sudo ufw status verbose`
```  
Status: active
Logging: on (low)
Default: deny (incoming), allow (outgoing), disabled (routed)
New profiles: skip

To                         Action      From
--                         ------      ----
22/tcp (OpenSSH)           ALLOW IN    Anywhere                  
80/tcp                     ALLOW IN    Anywhere                  
443                        ALLOW IN    Anywhere                  
22/tcp (OpenSSH (v6))      ALLOW IN    Anywhere (v6)             
80/tcp (v6)                ALLOW IN    Anywhere (v6)             
443 (v6)                   ALLOW IN    Anywhere (v6)             
```
- To enable `sudo ufw enable`

- Install fail2ban and configure it to prevent `sudo apt install fail2ban` then  start the service:`sudo systemctl start fail2ban`
  - Check:`sudo systemctl status fail2ban`
 `sudo systemctl enable fail2ban` to enable the service.

  - Brute force ssh authentication attacks

    - create a jail.local file: `sudo vi /etc/fail2ban/jail.local`
    - Edit:
    ```
    [sshd]
    enabled = true
    port = ssh
    logpath = /var/log/auth.log
    maxretry = 5
    bantime = 3600
    findtime = 600
    ```

- Exempt Applewood, Yard and Trio from sshd bans. For remote Quatrix interns, exempt your home network from fail2ban rules.
```
sudo cat /etc/fail2ban/jail.local
[sshd]
enabled = true
port = ssh
logpath = /var/log/auth.log
maxretry = 5
bantime = 1h
findtime =10m

[DEFAULT]
ignoreip = 197.232.110.49
```
### CI/CD - Jenkins

1. Install Jenkins

  - **Installing java:**
```
sudo apt update
sudo apt install fontconfig openjdk-21-jre
```

 - To check the java version installed: `java -version `

- **Installing Jenkins:**

- Downloading the Jenkins GPG key:
`sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc https://pkg.jenkins.io/debian-stable/jenkins.io-2026.key`   - Downloaded the official Jenkins signing key and saved it to the keyrings directory.APT needs this key to verify the authenticity of Jenkins packages when installing/updating.
- `sudo mkdir -p /etc/apt/keyrings` - Created a directory to store repository GPG keys.APT repositories require a key to verify downloaded packages
- **Adding the Jenkins repository:**
`echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian binary/" | sudo tee /etc/apt/sources.list.d/jenkins.list`  - Without this repository, apt wouldn’t know where to get Jenkins packages from.
- `sudo apt update` -Updating the package list
- `sudo apt install jenkins -y` Installing Jenkins
- `sudo systemctl start jenkins`- Starting Jenkins
- `sudo systemctl enable jenkins` Enabling Jenkins at boot
- Checking Jenkins service status `sudo systemctl status jenkins`


2. **Configure nginx and certbot to use the domain name https://test.jenkins.quatrixglobal.com to access Jenkins installation (If an email address is requested during certificate creation, use support@quatrixglobal.com)**

1. Install Nginx: 
```
sudo apt update
sudo apt install nginx -y
```

- Nginx reverse proxy	-Jenkins runs on port 8080. Nginx listens on port 80/443 and forwards traffic to Jenkins. It also handles HTTPS termination.
- Certbot (Let’s Encrypt)	Provides a free SSL/TLS certificate, enabling HTTPS so traffic is encrypted.
- Domain name mapping	Makes Jenkins accessible via https://test.jenkins.quatrixglobal.com instead of http://your-server-ip:8080.


2. Create a Configuration File: This tells Nginx how to handle requests for your specific domain.
`sudo vi /etc/nginx/sites-available/jenkins`

Insert: 
```
server {
    listen 80;
    server_name test.jenkins.quatrixglobal.com;

    location / {
        proxy_pass http://localhost:8080;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

- server_name: The domain name your users will type.
- proxy_pass: Forwards requests from Nginx to Jenkins (running on localhost:8080).
- proxy_set_header: Ensures Jenkins receives the correct client IP and protocol info.

3. Activate the configuration
`sudo ln -s /etc/nginx/sites-available/jenkins /etc/nginx/sites-enabled/`

sudo nginx -t  # Tests for syntax errors
`sudo systemctl restart nginx`

4. Step 2: Secure with Certbot
Install Certbot:`sudo apt install certbot python3-certbot-nginx -y`

5. Run the Certificate Generator: This command talks to Let's Encrypt, verifies you own the domain, and automatically updates your Nginx file to use HTTPS.
`sudo certbot --nginx -d test.jenkins.quatrixglobal.com --email support@quatrixglobal.com --agree-tos --no-eff-email`
Step 3: Unlock Jenkins and Initial Setup
Get your Admin Password `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`
- Access Jenkins: Open your browser and go to https://test.jenkins.quatrixglobal.com.
- Setup Wizard:
Paste the password you just copied.
Select "Install Suggested Plugins." This installs the core tools (Git, Pipeline, etc.) needed for CI/CD.

- Create user accounts for everyone in the tech team and share the details with each of them.
  - Go to settings, manage jenkins, click on create user(+), add the credentials then click save
  - To assign roles: Go to settings, manage and assign roles, click on assign roles, then add user (the one created above) then tick the role you eant to assign to that user.

- Utilizing the GitHub repo that you created at the beginning of this practical assessment:
  - Create a multi-branch pipeline for this repo
  - Ensure that a Jenkins build is automatically triggered when changes are pushed to GitHub for this repo. Instructions for this:
  - Create a Jenkinsfile in your repo.
    - Generating ssh keys for jenkins: 
    `sudo -u jenkins ssh-keygen -t ecdsa`
    
    - Located in: `sudo cat /var/lib/jenkins/.ssh/id_ecdsa`
    - To test it: while in test-traccar: sudo -u jenkins ssh lwachira@test.traccar.quatrixglobal.com
    pipeline - jenkins