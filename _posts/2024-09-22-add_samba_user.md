[如何在Linux中向Samba添加删除用户](https://www.cnblogs.com/a5idc/p/13533610.html)
我们先讨论如何向Samba添加新用户。首先，创建一个新的用户账户，就像在任何Linux系统中一样。在本例中，我们创建一个名为"joe"的新用户账户。
```
$ adduser joe
```
接下来，使用'smbpasswd'命令为新用户分配samba密码，添加samba用户，如下所示。
```
$ sudo smbpasswd -a joe
你会被提示提供一个新的samba密码，然后确认，如下所示。
New SMB password:
Retype new SMB password:
added user joe.
```
一旦你创建了samba用户，你需要通过编辑samba smb.conf文件将他们添加到samba共享中，这是Samba的配置文件。滚动并找到samba共享，在本例中，是 "文档"，并将该用户追加到有效用户列表中，如下面配置中的第四行所示。
```
[documents]
comment = Departmental documents share
path = /srv/documents
valid users = joe
public = no
writable = yes
browsable = yes
```
现在保存更改并退出配置文件。为了使更改持续下去，重新启动Samba守护进程，如下所示。
$ sudo systemctl restart smb
将现有的本地用户添加到samba
如果您的系统上已经有一个现有用户，则将用户添加到samba相当简单。只需使用'smbpasswd '命令，如下所示：
$ sudo smbpasswd -a existing_user
然后修改配置文件，并将现有用户添加到有效samba用户列表中，如前所示。
valid users = existing_user
关于将用户添加到Samba版本4.x的一点
从Samba版本4.x和更高版本开始，Samba可以作为AD Domain Controller运行。对于创建的每个Samba用户，您都不需要在Linux中具有标准Linux或Unix用户。要将用户添加到Samba Active目录中，请使用显示的命令：
samba-tool user add username
删除samba用户
如果要从系统中删除或删除Samba用户，请使用带有-x选项的'smbpasswd'命令和用户名。
$ sudo smbpasswd -x joe
如果需要，可以使用userdel命令将用户连同主目录一起完全删除，如下所示：
$ sudo userdel -r joe
我们已经介绍了如何在Linux系统上添加和删除Samba用户。如前所述，与早期版本的Samba不同，Samba 4.x版现在支持通过Active Directory进行身份验证。

A5互联https://www.a5idc.net/
