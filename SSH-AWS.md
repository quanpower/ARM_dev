# chmod 400
chmod 400 smartlinkcloud.pem

# ssh
ssh -i ~/dev/AWS/smartlinkcloud.pem ubuntu@54.254.228.240

#if can not connect because of an old keygen use clear
ssh-keygen -f "/home/quanpower/.ssh/known_hosts" -R 54.254.228.240
