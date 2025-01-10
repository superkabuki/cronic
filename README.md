# cronic
sane auto-renew for certbot
# I like certbot, it just needs a easy way to renew certs.
---
# Requirements
1. Python 3.6+
2. openssl 
3. Any UNIX or Linux system using cron.
--- 
# Install
1. git clone the repo `git clone https://github.com/superkabuki/cronic`
2. chmod cronic/cronic  `chmod +x cronic/cronic`
3. as root, run it with the path to your cert `cronic/cronic /etc/letsencrypt/live/example.com/cert.pem`
4. run it once and you're done.  It doesn't matter if you cert is up for renewal or not, cronic will handle it.
---



# Here's how certbot say to renew a cert

![image](https://github.com/user-attachments/assets/1c1d8bc7-a170-4e77-b451-f42f0ad16582)

# I disagree with this approach for a few reasons.
* I don't really understand the command. Why start a process and put it to sleep before doing anything?
* Attempting renewal on the 12th of every month creates a ton of traffic on their servers.
* The date is right there on the cert, cron uses dates, why not use it?

# cronic does it differently.

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

* You only have to run cronic manually once

* pass in the cert.pem file on the command line.


![image](https://github.com/user-attachments/assets/b3954ef6-957c-4f6b-8080-dca1865c6a1b)


* This cert expires on  Wed Apr  9 00:26:45 2025
* cronic set a cron job to renew on  Fri, 04 Apr 2025 17:36:23
* If cronic can't renew at that time, it will retry every four hours until it does renew.



