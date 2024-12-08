```
[sharename]
comment = 
path = /mnt
browsable = yes
guset ok = yes
read only = no
create mask = 0755
```
```
[z]
Comment = U-disk folder
Path = /media/devmon/z
valid users = x
Browseable = yes
Writeable = yes
only guest = no
create mask = 0777
directory mask = 0777
Public = yes
Guest ok = yes
```
```
sudo systemctl restart smbd
sudo systemctl enbale smbd

sudo useradd -m x
sudo passwd x 
```
===============================
```
[z]
Comment = U-disk folder
Path = /media/z
browseable = yes
read only = no
create mask = 0755
Guest ok = yes
```
```
mkdir -p /media/z
chown nobody:nogroup /media/z
sudo systemctl restart smbd.service nmbd.service
```
