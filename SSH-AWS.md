# chmod 400
chmod 400 smartlinkcloud.pem

# ssh
ssh -i ~/dev/AWS/smartlinkcloud.pem ubuntu@54.254.228.240

#if can not connect because of an old keygen use clear
ssh-keygen -f "/home/quanpower/.ssh/known_hosts" -R 54.254.228.240

# fanqiang

## use ssh connect aws ec2
	cd ~/.ssh
	vim config

	Host aws
	HostName 54.254.228.240
	User ubuntu
	IdentityFile ~/.ssh/smartlinkcloud.pem
	CompressionLevel 6
	DynamicForward localhost:3128
## edit proxy,or use autoproxy plugin

