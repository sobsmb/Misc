##################################################################################################################################
# Source: https://automatedhome.party/2023/07/11/automatically-backup-your-klipper-config-to-github-to-maintain-a-version-history/
##################################################################################################################################

# Enter Each Command:

cd ~/printer_data/config
git init
git add ~/printer_data/config/*
git config --global user.email "EMAIL@ADDRESS.YOURS"
git config --global user.name "YOUR NAME"
git commit -m "initial upload"
git config --global credential.helper store
git remote add origin https://github.com/USERNAME/PROJECT.git
git branch -M main
git push -f origin main

##################################################
# YOU WILL BE ASKED FOR YOUR USERNAME/ACCESS TOKEN
##################################################

nano ~/klipperBackup.sh


#################################
# IN THE FILE PAST THE FOLLOWING
#################################
#!/bin/sh
git -C ~/printer_data/config add ~/printer_data/config/.
git -C ~/printer_data/config commit -m "`date`"
git -C ~/printer_data/config push -u origin main
##################################


chmod +x ~/klipperBackup.sh
~/klipperBackup.sh
crontab -e

#####################
# SELECT NANO
# ENTER AT THE BOTTOM
#####################

*/30 * * * * ~/klipperBackup.sh

