
## Practical Assessment #1 - Test Traccar

### Basic Linux Administration

- Access:
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
- Check the current version of:
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