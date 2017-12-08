#samba服务器的搭建与配置

**操作系统：ubuntu16.04（32位）**

[TOC]

##准备工作
###1、添加新用户newUserName，并根据提示设置新用户的密码newUserPassword:
```
sudo adduser newUserName
注意：sudo deluser newUserName可以删除用户newUserName;
```
###2、设置用户目录权限：
现在home目录下应该已经存在文件夹newUserName,现在需要设置文件夹访问权限：
```
sudo chmod o+w newUserName -R
注意：命令行这里的newUserName就是新用户目录的名字；
```

##安装并配置samba
###1、命令行安装samba:
```
 sudo apt install samba
```
###2、将上面新增的用户newUserName添加至samba中，并根据提示设置密码：
```
sudo smbpasswd -a newUserName
注意：sudo smbpasswd -x newUserName可以将用户newUsesrName从samba中删除；
```
###3、修改samba配置文件：
```
sudo vi /etc/samba/smb.conf

添加如下内容至文件末尾：
[newUserName]
   comment =  newUserName's home directory
   browseable = yes
   path = /home/newUserName/
   guest ok = yes
   read only = no
   create mask = 0766
   directory mask = 0766
```

##结束
1、至此,在局域网内其它机器上利用samba客户端通过上边添加的samba用户名以及设置的密码即可对/home/newUserName/目录进行读写访问控制了。