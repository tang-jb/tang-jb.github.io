# 安装transmission-daemon 

比较乱，命令都在了。参考用。

sudo apt install transmission-daemon


You now must decide whether you want the desktop UI or just the web interface.

To install Transmission with its desktop interface, use the following command.

sudo apt install transmission
Copy
Alternatively, if you are running Ubuntu server or just don’t need the GUI you can install the daemon version of Transmission by using the following. command.

sudo apt install transmission-daemon



sudo nano /etc/transmission-daemon/settings.json
Copy
4. With the file open, you will want to ensure that RPC is enabled. In our case, it already was enabled.

You can verify it is enabled by searching for the following setting and ensuring it is set to “true“.

    "rpc-enabled": true,


For example, if you want to whitelist “192.168.0.123“, you would use the following.

    "rpc-whitelist": "127.0.0.1,192.168.0.123",
Copy
6. Alternatively, you can disable the whitelist altogether by finding the option below and setting the value to “false“.


    "rpc-whitelist-enabled": true



. Your next step is to force a reload on Transmission so that it will pull in the configuration changes. You do not want to restart the service as it will reset your changes.

sudo systemctl reload transmission-daemon





10. If you are using Transmission, you will likely want it to start up in the background automatically.

The first thing we need to do is create a new user called “transmission“. You will need to ensure the directories you want to save your torrents to can be accessed by this user.

sudo adduser --system --group transmission


----
Creating the System Service Files
10. If you are using Transmission, you will likely want it to start up in the background automatically.

The first thing we need to do is create a new user called “transmission“. You will need to ensure the directories you want to save your torrents to can be accessed by this user.

sudo adduser --system --group transmission
Copy
11. Now copy the service from the Transmission repository we cloned to our Ubuntu device earlier to the “systemd” directory.


sudo cp ~/Transmission/daemon/transmission-daemon.service /lib/systemd/system/
Copy
12. Our next step is to enable our new service so that the Transmission daemon will start when your Ubuntu device powers on.

All we need to do to enable the service is to use the following command.

sudo systemctl enable transmission-daemon.service
Copy
13. Once the service is enabled, we can immediately start the Transmission daemon using the command below.

sudo systemctl start transmission-daemon.service
Copy
Enabling the Web Interface for Transmission

14. Before we can make changes to Transmission’s settings we will need to temporarily disable it. If we don’t stop the service it can automatically overwrite all of your settings changes.

You can stop the Transmission torrent client on your Ubuntu device using the below command.

sudo systemctl stop transmission-daemon.service
Copy
15. When you are using Transmission without the GUI, you must enable the web interface by modifying the settings file.

You can begin editing this settings file by using the following command.

sudo nano /home/transmission/.config/transmission-daemon/settings.json
Copy
16. With this file open, we must change a few different settings. The first open allows us to enable the web interface.

Find the following option within this file.

    "rpc-enabled": false,
Copy
Once you find the line above, you must replace “false” with “true“. Doing this will enable Transmissions web interface on Ubuntu.

    "rpc-enabled": true,
Copy
17. After enabling the remote access functionality, you must modify the whitelist. By default, only the localhost can connect to the web interface.

To change this, find the following line within the file.

    "rpc-whitelist": "127.0.0.1,::1",
Copy
To add a new IP address to the whitelist, you must add a comma to the end of the current list followed by the IP Address. You can also use an asterisk as a wildcard.

For example, if we wanted everyone on the “192.168.0.0” subnet to have access to Transmission’s web interface, we would change the above line to the following.

    "rpc-whitelist": "127.0.0.1,::1,192.168.*.*",
Copy
18. After editing the configuration file, you can save and quit by pressing CTRL + X, followed by Y, then the ENTER key.

19. We can now safely start the Transmission daemon again. However, this time, you can now access the web interface.

sudo systemctl start transmission-daemon.service
Copy
Accessing the Transmission Web Interface

Now that you have Transmission installed on your Ubuntu system let us move on to how to access its web interface.

The web interface is a key feature of Transmission and allows you to access it remotely and easily manage your torrents.

1. To access the Transmission web interface, you must know your Ubuntu device’s IP address.

We recommend setting up a static IP address on your Ubuntu device, as it will make accessing the torrent client easier in the future.

2. Once you know your Ubuntu machine’s IP address, access Transmission’s web interface by going to the following address.

Ensure that you replace “IPADDRESS” with the address for your machine.

http://IPADDRESS:9091



