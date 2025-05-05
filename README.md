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


# STEP 3: Clean DNS

sudo nano /usr/local/bin/cleardns.sh

# Restart DNS
sudo systemctl restart AdGuardHome

# cat /var/log/update-apt-only.log

sudo chmod +x /usr/local/bin/cleardns.sh
sudo chmod +x /usr/local/bin/update-apt-only.sh

# sudo crontab -e

0 6 * * * /usr/local/bin/update-apt-only.sh
30 6 * * * /usr/local/bin/cleardns.sh
