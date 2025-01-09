# cronic
sane auto-renew for certbot
# Here's how certbot say to renew a cert

![image](https://github.com/user-attachments/assets/1c1d8bc7-a170-4e77-b451-f42f0ad16582)

# I strongly disagree with this approach for numerous reasons.
# Including but not limited to:
#### The command makes no sense. Why start a process and put it to sleep before doing anything?

#### Blindly attempting renewal on the 12th of every month, creates a ton of useless traffic on their servers.

#### The date is right there on the cert, cron uses dates, why not use it?

# cronic does it differenty.

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

![image](https://github.com/user-attachments/assets/635fb10c-1408-40b2-a845-939e5e34981a)

* This cert expires on  Wed Apr  9 00:26:45 2025
* cronic set a cron job to renew on  Fri, 04 Apr 2025 17:36:23
* If cronic can't renew at that time, it will retry every four hours until it does renew.



