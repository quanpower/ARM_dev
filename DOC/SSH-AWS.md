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
## use 
ssh aws

## edit proxy,or use autoproxy plugin
add proxy server:
name:aws,server:127.0.0.1,port:3128,
edit AWS iptable rules:
add tcp rule,port:3128,0.0.0.0:can access anywhere
