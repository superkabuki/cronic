# cronic is auto-renew for certbot

# cronic does it differently.
* cronic uses the certificate notAfter date to determine when to renew.
* renewal is scheduled for 5 days before certificate notAfter date.
* After the certificate is renewed, cronic automatically sets the next cron job.
* cronic has automatic Let's Encrypt certificate discovery.
* cronic support multiple certificates with different renewal dates, on the same server.
* cronic restarts services that use the certificates.
---
## cronic Requirements
1. __Python 3.6+__
2. __OpenSSL__ 
3. Any __UNIX__ or __Linux__ system that uses __cron__.
4. __certbot__
--- 

# How to Use
1. __Install certbot__ as instructed in the certbot directions. If you already have certbot installed, cool.
2. __Download cronic__ 
```js
 curl https://raw.githubusercontent.com/superkabuki/cronic/refs/heads/main/cronic -o cronic
```
3. as root __install cronic__.
```js
install cronic /usr/local/bin
```
4. as root __run cronic__. cronic will find and check your cert renewal date. <br>If you have multiple certs, no problem. cronic will find them and set the proper renewal times for them. 
```js
cronic
```
### Automatic certificate renewal is useless<br> if the services that use the certificate are not restarted.

5.  To __restart a service__, such as nginx, after the cert is renewed,<br> pass the command to cronic using the __--restart__ switch
```js
# OpenBSD
root@iodisco[~] cronic --restart 'rcctl restart nginx'

# Linux
root@iodisco[~] cronic --restart 'nginx -s reload'

```
6. __Rerun cronic anytime__ you want, __Add restart commands anytime__ you want. cronic cleans up after itself. <br> To __remove a restart command__  run crontab -e and delete the lines you want to remove.
```js
crontab -e
```

7. __cronic help__
```js
cronic -h
```

---
  
## cronic conditionals
* You can run cronic manually at any time, it won't break itself.
* These are the conditionals used by cronic.

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
---  
<img width="1183" height="689" alt="image" src="https://github.com/user-attachments/assets/935466c1-ac1b-4cc5-8c35-fd146715a588" />





* Of course it runs on [__OpenBSD__](https://openbsd.org).
* Also tested on __Debian Sid__.



