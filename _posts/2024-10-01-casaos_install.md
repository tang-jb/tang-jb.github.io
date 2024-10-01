玩客云：

### 1、烧录底包，安装linux
利用芯片厂家的烧录工具**burn**
烧录 **arm_bian.img**

安装完之后，用root:1234 顺手添加一个用户 (adduser)，并且visudo 添加sudo权限。

### 2、安装nas
登录linux，在线安装casaos
```
 sudo curl -fsSL https://get.casaos.io | sudo bash
```

