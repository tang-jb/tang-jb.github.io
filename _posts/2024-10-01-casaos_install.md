玩客云：

### 1、烧录底包，安装linux
利用芯片厂家的烧录工具**burn**
烧录 **arm_bian.img**

安装完之后，用root:1234 顺手添加一个用户 (adduser)，并且visudo 添加sudo权限。

### 2、安装nas
登录linux，在线安装casaos。虽然后继工作都是在linux上进行，但是casaos提供了一个web界面，部分解决了无头服务器的界面。安装后占用空间1.55g。
```
 sudo curl -fsSL https://get.casaos.io | sudo bash
```

### 3、安装samba


### 4、安装 打印机 hplip
