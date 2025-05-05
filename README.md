# Ubuntu-Auto-Update-With-Logs
Ubuntu Auto Update With Logs using Cron Tab


sudo nano /usr/local/bin/update-apt-only.sh

#!/bin/bash

# Log file
LOGFILE="/var/log/update-apt-only.log"

echo "🔧 Starting APT-only system update at $(date)" >> $LOGFILE
echo "---------------------------------------------" >> $LOGFILE

# STEP 1: Update & Upgrade
sudo apt update >> $LOGFILE 2>&1
sudo apt dist-upgrade -y >> $LOGFILE 2>&1

# STEP 2: Clean up
sudo apt autoremove -y >> $LOGFILE 2>&1
sudo apt autoclean -y >> $LOGFILE 2>&1

echo "✅ APT update done at $(date)" >> $LOGFILE



sudo nano /usr/local/bin/cleardns.sh

#!/bin/bash
sudo systemctl restart AdGuardHome


cat /var/log/update-apt-only.log


sudo chmod +x /usr/local/bin/cleardns.sh
sudo chmod +x /usr/local/bin/update-apt-only.sh

sudo crontab -e

# Edit this file to introduce tasks to be run by cron.
#
# Each task to run has to be defined through a single line
# indicating with different fields when the task will be run
# and what command to run for the task
#
# To define the time you can provide concrete values for
# minute (m), hour (h), day of month (dom), month (mon),
# and day of week (dow) or use '*' in these fields (for 'any').
#
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
0 6 * * * /usr/local/bin/update-apt-only.sh
30 6 * * * /usr/local/bin/cleardns.sh
