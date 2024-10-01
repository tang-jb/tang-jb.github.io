玩客云：

### 1、烧录底包，安装linux
利用芯片厂家的烧录工具**burn**
烧录 **arm_bian.img**

安装完之后，用root:1234 顺手添加一个用户 (adduser)，并且visudo 添加sudo权限。
登录工具使用git自带的mingw

### 2、安装nas
登录linux，在线安装casaos。虽然后继工作都是在linux上进行，但是casaos提供了一个web界面，部分解决了无头服务器的界面。并且也自带了部分傻瓜式操作。因此选择安装该nas。
安装后占用空间1.55g。
```
 sudo curl -fsSL https://get.casaos.io | sudo bash
```
大约半小时左右，下载安装完成。
用浏览器首次登录casaos需要设置casaos的用户密码。选择与linux同名用户。

### 3、设置samba
samba系统已经安装，需要设置一下。因为本系统会自动把插入的u盘挂载到/media/xxx/ulabel下，
所以预先设定u盘label为z，这样固定挂载到/media/xxx/z/下。

```
[hole]
Comment = 2nd Shared U-disk folder
Path = /media/hole
Browseable = yes
Writeable = yes
only guest = no
create mask = 0777
directory mask = 0777
Public = yes
Guest ok = yes

```

### 4、安装 打印机 hplip
