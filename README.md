# One_Line_Crontab_OpenVPN_Connection_Monitor
Checks for the existence of network device (tap0) and restarts the system if it doesn't.

OpenVPN may lose connection for various reasons. After having gotten my connection very stable, I still experience drops at least once a week. To combat this, the only thing I've come up with is to just give the system a quick restart.

I don't want to wait for scheduled restarts if something goes wrong though and want to check the system every 5mins for connectivity. 
I've found that the network device created for my TAP connection disappears when my connection does. Probing for this, a restart command can be issued in one line (technically 2) in Crontab.

# Crontab entry:

#!/bin/bash
# Edit this file to introduce tasks to be run by cron.
#
# Each task to run has to be defined through a single line
# indicating with different fields when the task will be run
# and what command to run for the task
#
# To define the time you can provide concrete values for
# minute (m), hour (h), day of month (dom), month (mon),
# and day of week (dow) or use '*' in these fields (for 'any').#
# Notice that tasks will be started based on the cron's system
# daemon's notion of time and timezones.
#
# Output of the crontab jobs (including errors) is sent through
# email to the user the crontab file belongs to (unless redirected).
#
# For example, you can run a backup of all your user accounts
# at 5 a.m every week with:
# 0 5 * * 1 tar -zcf /var/backups/home.tgz /home/
#
# For more information see the manual pages of crontab(5) and cron(8)
#
# m h  dom mon dow   command
SHELL=/bin/bash
*/5 * * * * if [ "$(cat /sys/class/net/tap0/operstate)" = "unknown" ]; then date; else sudo shutdown -r now; fi
