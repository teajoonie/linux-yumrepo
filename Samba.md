# 服务端的samba配置
查看Linux是否安装了Samba
```
rpm -qa | grep samba
```
yum安装samba
```
yum install -y samba
```

服务端Samba修改其配置文件，文件目录位置：`/etc/samba/samba.conf`
```
[share]                                <==共享资源名称
        comment = kaskdjhsjadksjdbas   <==共享说明
        path = /tmp                    <==实际的共享目录
        writable = yes                 <==设置为可写入
        browseable = yes               <==可以被所有用户浏览到资源名称，
        valid users = testuser         <==设置访问用户，如果设置允许组则@组名，空格分隔多个用户、组名
```

添加Samba用户并设置密码，需要先设置系统用户再设为Sambe用户，配置成Samba用户时，需要设置Samba用户的密码
```
useradd testuser    ---系统添加用户  -s /sbin/nologin 创建的用户不可见
smbpasswd -a testuser     ---将系统用户添加为Samba用户，并要求设置Samba用户的密码
```
重启Samba服务器，使其新配置生效（如果之前已经启动samba服务了）
```
systemctl restart smb
```
# 客户端的Samba连接
查看Samba允许的用户查看其允许查看的文件
```
smbclient -L //Samba服务端IP -U testuser
```
1.普通连接samba服务端
```
smbclient -U testuser //samba服务端IP/共享资源名称   ---要去输入Samba用户testuser的Samba用户密码
```
2.将Samba服务端共享资源挂载到本地目录建立连接
```
mkdir /data/share    ---本地创建挂载点
mount //Samba服务端IP/共享资源名称 /data/share -o username=testuser,password=Samba用户设置的Samba用户密码
```
删除挂载点以退出对于Samba服务的文件共享
```
umount /data/share
```
