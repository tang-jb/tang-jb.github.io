samba添加用户 原创 [原文地址](https://blog.51cto.com/gavin0/2061647)
魔都搬砖2018-01-16 17:04:04博主文章分类：【杂文】
文章标签samba添加用户文章分类运维阅读数10000+

1、首先新增linux的系统用户
useradd -G samba UserName echo 'Password' |passwd --stdin UserName
2、修改添加用户的共享目录的可写入权限
vim /etc/samba/smb.conf

3、添加smmba用户
smbpasswd -a UserName

4、重启smb服务
systemctl restart smb.service

企业案例

财务内控团队这边需要建一个公共盘，主要用于收集7个事业部（车险事业部、健康险事业部、金融事业部、电商事业部、航旅事业部、技术平台和运营平台）上传的文档资料。
其中7个事业部之间的访问需要进行隔离，本事业部的同事只能访问自己事业部的文件夹，而财务内控团队的同事不受此限制（需要由访问、下载等权限）

smb.conf配置文件添加一下配置信息
```

[public]  #财务部
comment = FinancialDepartment   #
public = no
browseable = no
guest ok = no
path = /etc/samba/public
valid users = FinancialDepartment
write list = FinancialDepartment
admin users = FinancialDepartment

[LifestyleConsumption]  #电商事业部
comment = LifestyleConsumption
public = no
browseable = no
guest ok = no
path = /etc/samba/public/LifestyleConsumption
valid users = LifestyleConsumption
write list = LifestyleConsumption
admin users = FinancialDepartment,LifestyleConsumption

[Travel]  #航旅
comment = Travel
public = no
browseable = no
guest ok = no
path = /etc/samba/public/Travel
valid users = Travel
write list = Travel
admin users = FinancialDepartment,Travel


[Health]  #健康险
comment = Health
public = no
browseable = no
guest ok = no
path = /etc/samba/public/Health
valid users = Health
write list = Health
admin users = FinancialDepartment,Health



[ConsumerFinance]  #金融技术部
comment = ConsumerFinance
public = no
browseable = no
guest ok = no
path = /etc/samba/public/ConsumerFinance
valid users = ConsumerFinance
write list = ConsumerFinance
admin users = FinancialDepartment,ConsumerFinance



[Auto]  #车险
comment = Auto
public = no
browseable = no
guest ok = no
path = /etc/samba/public/Auto
valid users = Auto
write list = Auto
admin users = FinancialDepartment,Auto



[TechnicalPlatform]  #技术平台
comment = TechnicalPlatform
public = no
browseable = no
guest ok = no
path = /etc/samba/public/TechnicalPlatform
valid users = TechnicalPlatform
write list = TechnicalPlatform
admin users = FinancialDepartment,TechnicalPlatform



[OperationPlatform_OP]  #运营平台-开放平台
comment = OperationPlatform_OP
public = no
browseable = no
guest ok = no
path = /etc/samba/public/OperationPlatform_OP
valid users = OperationPlatform_OP
write list = OperationPlatform_OP
admin users = FinancialDepartment,OperationPlatform_OP

[OperationPlatform_TD]  #运营平台-运营技术
comment = OperationPlatform_TD
public = no
browseable = no
guest ok = no
path = /etc/samba/public/OperationPlatform_TD
valid users = OperationPlatform_TD
write list = OperationPlatform_TD
admin users = FinancialDepartment,OperationPlatform_TD
1.
2.
3.
4.
5.
6.
7.
8.
9.
10.
11.
12.
13.
14.
15.
16.
17.
18.
19.
20.
21.
22.
23.
24.
25.
26.
27.
28.
29.
30.
31.
32.
33.
34.
35.
36.
37.
38.
39.
40.
41.
42.
43.
44.
45.
46.
47.
48.
49.
50.
51.
52.
53.
54.
55.
56.
57.
58.
59.
60.
61.
62.
63.
64.
65.
66.
67.
68.
69.
70.
71.
72.
73.
74.
75.
76.
77.
78.
79.
80.
81.
82.
83.
84.
85.
86.
87.
88.
89.
90.
91.
92.
93.
94.
95.
96.
97.
98.
[分享的资源名称]
<指令1>; = (参数)
<指令2>; = (参数)

要提供分享资源时，须先把欲分享的资源以 [ ] 符号括住，底下通常会带指令和参数来表示此资源的设定和存取权限等，详情如下：

comment---------注释说明
path------------分享资源的完整路径名称，除了路径要正确外，目录的权限也要设对
browseable------是yes/否no在浏览资源中显示共享目录，若为否则必须指定共享路径才能存取
printable-------是yes/否no允许打印
hide dot ftles–是yes/否no隐藏隐藏文件
public----------是yes/否no公开共享，若为否则进行身份验证(只有当security = share 时此项才起作用)
guest ok--------是yes/否no公开共享，若为否则进行身份验证(只有当security = share 时此项才起作用)
read only-------是yes/否no以只读方式共享当与writable发生冲突时也writable为准
writable--------是yes/否no不以只读方式共享当与read only发生冲突时，无视read only
vaild users-----设定只有此名单内的用户才能访问共享资源(拒绝优先)(用户名/@组名)
invalid users—设定只有此名单内的用户不能访问共享资源(拒绝优先)(用户名/@组名)
read list-------设定此名单内的成员为只读(用户名/@组名)
write list------若设定为只读时，则只有此设定的名单内的成员才可作写入动作(用户名/@组名)
create mask-----建立文件时所给的权限
directory mask–建立目录时所给的权限
force group-----指定存取资源时须以此设定的群组使用者进入才能存取(用户名/@组名)
force user------指定存取资源时须以此设定的使用者进入才能存取(用户名/@组名)
allow hosts-----设定只有此网段/IP的用户才能访问共享资源
allwo hosts = 网段 except IP
deny hosts------设定只有此网段/IP的用户不能访问共享资源
allow hosts=本网段指定IP指定IP
deny hosts=指定IP本网段指定I
```
