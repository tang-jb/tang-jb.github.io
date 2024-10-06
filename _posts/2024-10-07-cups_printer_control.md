use cups cli control the printer to print files

[source](https://docs.oracle.com/cd/E26926_01/html/E25812/gllgm.html)



```
lp -P listPages
$ lpstat -p printer-name -l
$ lpoptions -d printer-name
$ lpstat -p printer-name
$ lp -d destination-printer filename

$ lpstat -d

$ lpstat [-d] [-p] printer-name [-l] [-t]
-d
显示系统的缺省打印机。

-p printer-name
显示打印机是处于活动状态还是空闲状态以及启用或禁用打印机的时间。

您可以使用此命令指定多个打印机名称。使用空格或逗号来分隔打印机名称。如果您使用空格，请用引号将打印机名称列表引起来。如果不指定 printer-name，将显示所有打印机的状态。

-l
显示打印机和作业的特征。

-t
```

```lp -n 5 filename.pdf```
这个命令会打印文件filename.pdf的前5页。

```

复制
# 查看打印队列状态
lpstat -o

# 取消错误的打印任务
cancel -a
```
