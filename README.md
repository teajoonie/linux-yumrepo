# Centos-linux-yumrepo
yum-localrepos-seting

yum repolist
cd /etc/yum.repos.d/
ls
mkdir backup/
mv Centos-* backup/
touch local.repo
vim local.repo
  ---here is its content---
  [local]
  name=local
  baseurl=file:///media/cdrom
  enable=1
  gpgcheck=0
mkdir -p /media/cdrom
mount /dev/cdrom /media/cdrom
df -h
vim /etc/fstab
  ---here is its content---
  /dev/cdrom  /media/cdrom  iso9660  defaults  0 0
yum repolist
yum install httpd
