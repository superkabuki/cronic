# cronic
sane auto-renew for certbot
### I like certbot, it just needs an easy way to renew certs.

## cronic Requirements

1. Python 3.6+
2. openssl 
3. Any UNIX or Linux system using cron.
4. certbot
--- 
## Install cronic

1. git clone the repo `git clone https://github.com/superkabuki/cronic`
2. chmod cronic/cronic  `chmod +x cronic/cronic`
3. as root, run it. `cronic/cronic `
4. run it once and you're done.
   * It doesn't matter if you cert is up for renewal or not.
   * It doesn't matter how many certs you have, cronic will handle it.
---

# Here's how certbot say to renew a cert

![image](https://github.com/user-attachments/assets/1c1d8bc7-a170-4e77-b451-f42f0ad16582)

# I disagree with this approach for a few reasons.
* I don't really understand the command. Why start a process and put it to sleep before doing anything?
* Attempting renewal on the 12th of every month creates a ton of traffic on their servers.

# cronic does it differently.
* The date is right there on the cert, cron uses dates, why not use it?
* cronic has automatic Let's Encrypt cert discovery.
* cronic support multiple certs with different renewals, on the same server.

* __If it's too early to renew the cert__: 
  * let's encrypt is not contacted. 
  * Cron job installed to valid renewal time.
  * crontab displayed.

* __If renewal fails__:
  * error messages printed.
  * new cronjob installed for four hours later.
  * crontab displayed.

* __If renewal time is valid__:
  * cert is renewed.
  * cron job created for next renewal at valid renewal time.
  * crontab displayed.

* You only have to run cronic manually once.
![image](https://github.com/user-attachments/assets/cb436eea-4249-4e1b-b2f7-0a86f45e30d0)

* Of course it Runs on OpenBSD.
* Also tested on Debian Sid.


* This cert expires on  Wed Apr  9 00:26:45 2025
* cronic set a cron job to renew on  Fri, 04 Apr 2025 17:36:23
* If cronic can't renew at that time, it will retry every four hours until it does renew.



