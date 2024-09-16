[sharename]
comment = 
path = /mnt
browsable = yes
guset ok = yes
read only = no
create mask = 0755

sudo systemctl restart smbd
sudo systemctl enbale smbd

sudo useradd -m x
sudo passwd x 
