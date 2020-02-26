# One_Line_Crontab_OpenVPN_Connection_Monitor
Checks for the existence of network device (tap0) and restarts the system if it doesn't.

OpenVPN may lose connection for various reasons. After having gotten my connection very stable, I still experience drops at least once a week. To combat this, the only thing I've come up with is to just give the system a quick restart.

I don't want to wait for scheduled restarts if something goes wrong though and want to check the system every 5mins for connectivity. 
I've found that the network device created for my TAP connection disappears when my connection does. Probing for this, a restart command can be issued in one line (technically 2) in Crontab.

# Crontab entry:

SHELL=/bin/bash

*/5 * * * * if [ "$(cat /sys/class/net/tap0/operstate)" = "unknown" ]; then date; else sudo shutdown -r now; fi
