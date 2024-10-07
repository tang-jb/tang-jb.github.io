qlbittorren

[source](https://post.smzdm.com/p/a60rl4dz/)
[Unit]
Description=qBittorrent Daemon Service
After=network.target
[Service]
User=root
ExecStart=/usr/bin/qbittorrent-nox
ExecStop=/usr/bin/killall -w qbittorrent-nox
[Install]
WantedBy=multi-user.target

我们运行安装qb的命令：

apt install qbittorrent-nox

等待命令执行完即可。

安装完成后，我们创建qBittorrent这个服务，方便设置开机自启。

执行如下命令：

nano /etc/systemd/system/qbittorrent.service

然后将下面的内容粘贴并保存：

[Unit]
Description=qBittorrent Daemon Service
After=network.target
[Service]
User=root
ExecStart=/usr/bin/qbittorrent-nox
ExecStop=/usr/bin/killall -w qbittorrent-nox
[Install]
WantedBy=multi-user.target

执行下面的命令更新服务：

systemctl daemon-reload

常用命令
启动qb
service qbittorrent start

关闭qb
service qbittorrent stop

查看qb状态
service qbittorrent status

开机自启
systemctl enable qbittorrent

关闭开机自启
systemctl disable qbitorrent
