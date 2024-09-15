sudo systemctl restart cups

remote access cups through web

3 methods:

1.
cupsctl --remote-admin --remote-any --share-printers
it will update the /etc/cups/cupsd.conf file and restart cups for you, saving a backup of the previous configuration in the same folder.

http://www.cups.org/documentation.php/doc-2.0/sharing.html

2.
ssh admin@10.36.8.43 -T -L 3631:localhost:631

3.
http://thismightbehelpful.blogspot.com/2008/09/remote-access-tocups-web-interface.html
Allow all to <Location /admin>

Allow from 192.168.8.114  #a certain computer
Allow from 192.168.8.*    #subnet


---
sudo usermod -aG lpadmin username
sudo systemctl restart cups

sudo ufw allow 631/tcp

sudo apt install avahi-daemon -y
sudo systemctl start avahi-daemon
sudo systemctl enable avahi-daemon




----
[printers]
   comment = All printers
   path = /var/spool/samba
   printable = yes
   guest ok = no
   read only = yes
   create mask = 0700
   browseable = yes
   [print$]
   comment = Printer Drivers
   path = /etc/samba/drivers
   browseable = yes
   guest ok = no
   read only = yes
   create mask = 0700


   ----
   三、安装打印机服务器

我的打印机是HP 1010，型号比较老。

1、开粘命令：

安装cups打印服务：

apt-get install cups

安装完后，开始参数配置（我也不懂），在这里鼠标不管用，所以不用点，用键盘调位置：

nano /etc/cups/cupsd.conf

2、首先将Listen localhost:631修改为Listen 0.0.0.0:631

3、将Browsing No改成Browsing On

4、在以下四段增加Allow all

# Restrict access to the server...

  Order allow,deny

  Allow all

# Restrict access to the admin pages...

  Order allow,deny

  Allow all

# Restrict access to configuration files...

  AuthType Default

  Require user @SYSTEM

  Order allow,deny

  Allow all

# Restrict access to log files...

  AuthType Default

  Require user @SYSTEM

  Order allow,deny

 Allow all

5、按Ctrl+X，选择保存（Y），再按回车就回到命令行了；

6、重启CUPS服务：

service cups restart

7、安装打印机驱动，没有这一步，在浏览器里是看不到打印机的：

apt-get install hplip

输入d回车下载输入d回车下载

8、把打印机接盒子靠近HDMI那个USB口上，打印机开机；

9、安装hp-plugin：

hp-plugin

输入y回车，接受协议输入y回车，接受协议(hp-setup -i)
(lsusb)

10、安装打印机被发现服务：

apt-get -y install avahi-daemon avahi-discover libnss-mdns

systemctl restart avahi-daemon

service cups restart

11、最后设置下开机默认启动（好像不设置也可以开机启动）：

systemctl enable cups

systemctl enable avahi-daemon

12、到这一步，所有安装就完成了，再次输入下面命令退出putty：

exit
