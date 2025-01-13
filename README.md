# cronic auto-renew for certbot
![image](https://github.com/user-attachments/assets/2f166692-ec92-44e3-a3f9-be44d415a24b)

### Let me state emphatically***, I am a HUGE fan of certbot.
> I have always had a problem with companies charging hundreds of dollars for certs, and I used to self sign certs for my mail servers, and that huge pain in the ass. My only issue is that I often forget to renew my certs in a timely manner. I've been using this for a couple of years and haven't even thought about my certs until just recently when I deployed a new OpenBSD mail server, I ran certbot got my cert, ran cronic and set a cron job, and I'm done. 
<br>
>_I can't believe I spelled emphatically correctly, on the first try._


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

