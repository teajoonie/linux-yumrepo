# Centos-linux-yumrepo
yum-localrepos-seting  
查看仓库  
```yum repolist ```
进入yum仓库配置区  
```cd /etc/yum.repos.d/  ```
查看仓库文件  
```ls  ```
创建备份文件夹  
```mkdir backup/ ```
将其所有原配置文件放入backyup目录进行备份  
```mv Centos-* backup/```
创建本地源文件并编辑
```
touch local.repo  
vim local.repo  
  ---here is its content---  
  [local]  
  name=local  
  baseurl=file:///media/cdrom  
  enable=1  
  gpgcheck=0  
```
创建本地源仓库挂载目录并挂载
```
mkdir -p /media/cdrom  
mount /dev/cdrom /media/cdrom  
```
查看挂载
```
df -h
```
设置其挂载开机自动挂载
```
vim /etc/fstab  
  ---here is its content---  
  /dev/cdrom  /media/cdrom  iso9660  defaults  0 0  
```
查看仓库
```yum repolist  ```
通过yum仓库进行httpd下载
```yum install httpd  ```
