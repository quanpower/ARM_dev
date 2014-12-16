# mount 
sudo mount -t vboxsf VM_FTP /mnt/share

# add group
sudo adduser "quanpower" vboxsf

# auto mount
要想自动挂载的话，可以在/etc/fstab中添加一项
VM_FTP /mnt/shared vboxsf rw,gid=100,uid=1000,auto 0 0
## or:
在文件 /etc/rc.local 中（用root用户）追加如下命令
mount -t vboxsf VM_FTP /mnt/share
