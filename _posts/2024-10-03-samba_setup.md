samba perameters

[source](https://handerfly.github.io/%E8%BF%90%E7%BB%B4/2019/08/29/samba/)

[configure samba as a fioe server ](https://ubuntu.com/tutorials/install-and-configure-samba#1-overview)


Configure Samba as a file server
The main Samba configuration file is located in /etc/samba/smb.conf. The default configuration file contains a significant number of comments, which document various configuration directives.

Note:
Not all available options are included in the default configuration file. See the smb.conf man page or the Samba HOWTO Collection for more details.

First, edit the workgroup parameter in the [global] section of /etc/samba/smb.conf and change it to better match your environment:

workgroup = EXAMPLE
Create a new section at the bottom of the file, or uncomment one of the examples, for the directory you want to share:

'''
[share]
    comment = Ubuntu File Server Share
    path = /srv/samba/share
    browsable = yes
    guest ok = yes
    read only = no
    create mask = 0755

'''
comment
A short description of the share. Adjust to fit your needs.

path
The path to the directory you want to share.

Note:
This example uses /srv/samba/sharename because, according to the Filesystem Hierarchy Standard (FHS), /srv is where site-specific data should be served. Technically, Samba shares can be placed anywhere on the filesystem as long as the permissions are correct, but adhering to standards is recommended.

browsable
Enables Windows clients to browse the shared directory using Windows Explorer.

guest ok
Allows clients to connect to the share without supplying a password.

read only determines if the share is read only or if write privileges are granted. Write privileges are allowed only when the value is no, as is seen in this example. If the value is yes, then access to the share is read only.

create mask
Determines the permissions that new files will have when created.

Create the directory
Now that Samba is configured, the directory needs to be created and the permissions changed. From a terminal, run the following commands:

'''
sudo mkdir -p /srv/samba/share
sudo chown nobody:nogroup /srv/samba/share/
'''

The -p switch tells mkdir to create the entire directory tree if it doesn’t already exist.

Enable the new configuration
Finally, restart the Samba services to enable the new configuration by running the following command:

'''
sudo systemctl restart smbd.service nmbd.service
'''

