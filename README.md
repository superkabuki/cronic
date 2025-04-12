# cronic is auto-renew for certbot
![image](https://github.com/user-attachments/assets/2f166692-ec92-44e3-a3f9-be44d415a24b)

# Cron based automatic certificate discovery and renewal. 

![image](https://github.com/user-attachments/assets/5166c335-d5de-4933-b1a5-b68336072a68)

# cronic now restarts services.

![image](https://github.com/user-attachments/assets/8dd83c77-cf69-4be5-bd9f-16a1627264ca)

### Automatic certificate renewal is useless if the services that use the certificate are  not restarted.

* To have a service restarted after the certificate is renewed, use the "__--restart__" switch.
* __--restart__  is followed by the command in quotes.
* example:
  
```sh
    ./cronic --restart "/usr/sbin/nginx -s reload"
```
* __--restart__ commands can be added anytime, whether or not the certificate is renewed.

* __--restart__ commands only need to be added once.

* the command will be run after a certificate is renewed.

* to remove a restart command:
```sh
        crontab -e
```

* delete the line containing the command you wish to remove.




# cronic does it differently.

* cronic uses the certificate notAfter date to determine when to renew.
* renewal is scheduled for 5 days before certificate notAfter date.
* After the certificate is renewed, cronic automatically sets the next cron job.
* cronic has automatic Let's Encrypt certificate discovery.
* cronic support multiple certificates with different renewal dates, on the same server.
  
## cronic conditionals
* You can run cronic manually at any time, it won't break itself.
* These are the conditioals used by cronic.

* __If the cert IS ready for renewal__:
  * cert is renewed.
  * cron job created for next renewal at valid renewal time.
  * crontab displayed.
  * servicess are restarted to use the new certificate.
  
* __If the cert is NOT ready renewal__: 

  * let's encrypt is not contacted. 
  * Cron job installed to valid renewal time.
  * crontab displayed.

* __If the renewal process fails and renewal cannot be attempted__:
  * error messages printed.
  * new cronjob installed for four hours later.
  * crontab displayed.
  



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

