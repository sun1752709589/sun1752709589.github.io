---
layout: post
title: Ubuntu使用笔记
---

我的Ubuntu使用笔记

### 二台机器之间同步大文件(拷贝文件到另一台机器)
rsync -rP --rsh=ssh /file/path name@ip:/file/path
### 建立软连接
ln -s original/file/path soft/file/path
### linux后台启动服务
nohup ruby http_server.rb 2>&1 >> log.log 2>&1 /dev/null &
nohup command &> /dev/null &
### linux根据关键字得到pid号
pgrep -f keyword
### linux创建sudo用户
adduser username
usermod -aG sudo username
### sudo免密码
vi /etc/sudoers
root    ALL=(ALL:ALL) ALL
deployer ALL=(ALL) NOPASSWD: ALL
%admin ALL=(ALL) NOPASSWD: ALL
%sudo   ALL=(ALL:ALL) NOPASSWD: ALL
### virtualbox安装VboxLinuxAdditions
```
# prepare
$ sudo apt-get install -y linux-headers-generic build-essential dkms
# get the right ISO from http://download.virtualbox.org/virtualbox/
$ wget http://download.virtualbox.org/virtualbox/5.1.6/VBoxGuestAdditions_5.1.6.iso
# create a mount folder
$ sudo mkdir /media/VBoxGuestAdditions
# mount the ISO
$ sudo mount -o loop,ro VBoxGuestAdditions_5.1.6.iso /media/VBoxGuestAdditions
# install the guest additions
$ sudo sh /media/VBoxGuestAdditions/VBoxLinuxAdditions.run
# remove the ISO
$ rm VBoxGuestAdditions_5.1.6.iso
# unmount the ISO
$ sudo umount /media/VBoxGuestAdditions
# remove the mount folder
$ sudo rmdir /media/VBoxGuestAdditions
```
### Ubuntu增加虚拟内存
```
docker run --name caravel -d -p 8088:8088 amancevice/caravel
docker exec -it caravel demo

设置swappiness的值
swappiness 可以具有介于 0 和 100 之间的值
swappiness = 0 告诉内核尽可能长时间避免交换物理内存的过程
swappiness = 100 告诉内核积极交换物理内存的进程，并将它们交换缓存移动
cat /proc/sys/vm/swappiness
sudo sysctl vm.swappiness=66
sudo vi /etc/sysctl.conf
文档的尾部追加:
vm.swappiness=66

增加虚拟内存
dd if=/dev/zero of=/swap/swapadd bs=1024 count=2097152  # 2GB
mkswap /swap/swapadd
swapon /swap/swapadd

change conf file /etc/fstab
/swap/swapadd none swap sw 0 0

关闭虚拟内存服务
swapoff -v /swap/swapadd

如果当前的虚存所在的磁盘空间不够，可以首先关闭虚存服务，将其移动到别的磁盘，再启用即可。
swapoff -v /swap/swapadd
mv /swap/swapadd /mnt/swap
swapon /swap/swapadd
```
### supervisor使用
```
sudo pip install supervisor
conf file: /etc/supervisord.conf
$ supervisorctl status
$ supervisorctl stop usercenter
$ supervisorctl start usercenter
$ supervisorctl restart usercenter
$ supervisorctl reread
$ supervisorctl update
```
### linux手动释放内存
```
释放前最好sync一下，防止丢数据。
cache释放：
To free pagecache:
echo 1 > /proc/sys/vm/drop_caches

To free dentries and inodes:
echo 2 > /proc/sys/vm/drop_caches

To free pagecache, dentries and inodes:
echo 3 > /proc/sys/vm/drop_caches
```