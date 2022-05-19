#1.下载NFS服务
###Centos
Centos服务器端nfs安装
```
yum install nfs-utils rpcbind
```
Centos客户端nfs安装
```
yum install nfs-utils
```
###Ubuntu
Ubuntu服务器nfs安装
```
apt install nfs-kernel-server
```
Ubuntu客户端nfs安装
```
apt install nfs-common
```
####2.服务器端/etc/exports文件配置
```
vim /etc/exports
  ---here is its content---
  /data/share 192.168.160.0/24(rw,sync) ---
                                        ro 该主机对该共享目录有只读权限
                                        rw 该主机对该共享目录有读写权限
                                        root_squash 客户机用root用户访问该共享文件夹时，将root用户映射成匿名用户
                                        no_root_squash 客户机用root访问该共享文件夹时，不映射root用户
                                        all_squash 客户机上的任何用户访问该共享目录时都映射成匿名用户
                                        anonuid 将客户机上的用户映射成指定的本地用户ID的用户
                                        anongid 将客户机上的用户映射成属于指定的本地用户组ID
                                        sync 资料同步写入到内存与硬盘中
                                        async 资料会先暂存于内存中，而非直接写入硬盘
                                        insecure 允许从这台机器过来的非授权访问
                                        crossmnt 客户端可以访问所有挂载在文件系统上并标记有crossmnt的文件系统并且客户端不需要单独逐个挂载子共享. 请注意,你可能不希望在子共享同时被共享到另一端地址时使用该选项.
```
####3.创建nfs共享文件目录
```
mkdir /data/share
```
__请确认此文件的权限__
####4.重启nfs服务
```
systemctl restart nfs
---Ubuntu的nfs服务名为nfs-kernel-server
```
####5.查看共享文件目录
```
showmont -e
```
###客户端
打开nfs服务
```
systemctl restart nfs
---Ubuntu的nfs服务名为nfs-kernel-server
```
查看共享文件目录
```
showmont -e 
或者
showmont -e 服务端IP
```
创建本地挂载目录以挂载nfs共享文件目录
```
mkdir /data/share
```
挂载服务端共享文件目录到本地挂载目录
```
mount -t nfs 服务端IP:/data/share /data/share

ls /data/share
```

