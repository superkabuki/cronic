# cronic
sane auto-renew for certbot

### certbot says:

![image](https://github.com/user-attachments/assets/1c1d8bc7-a170-4e77-b451-f42f0ad16582)

# cronic does it differently.

* cronic uses the certificate notAfter date to determine when to renew.
* renewal is scheduled for 5 days before certificate notAfter date.
* After the certificate is renewed, cronic automatically sets the next cron job.
* cronic has automatic Let's Encrypt certificate discovery.
* cronic support multiple certificates with different renewal dates, on the same server.
  
## cronic conditionals

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


  

![image](https://github.com/user-attachments/assets/834c0793-b182-4895-a67e-fc52cf295249)


* Of course it runs on [__OpenBSD__](https://openbsd.org).
* Also tested on __Debian Sid__.



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
   * It doesn't matter if you cert is up for renewal or not, cronic will handle it.
   * It doesn't matter how many certs you have, cronic will handle it.
---

