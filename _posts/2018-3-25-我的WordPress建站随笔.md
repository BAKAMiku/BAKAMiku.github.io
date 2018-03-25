---
layout:     post
title:      WordPress建站随笔
subtitle:   我的WordPress建站随笔
date:       2018-03-25
author:     Zachary
header-img: img/post-bg-coffee.jpg
catalog: true
tags:
    - server
    - ssh
    - wordpress
---

### Linux 常用命令
```
cd xxx//进入本目录下的 xxx 文件夹中
cd ..//返回上一层菜单

logout//退出登录
```

### 创建密钥对
```
~ ssh-keygen
Generating public/private rsa key pair.

Enter file in which to save the key (/home/bakamiku/.ssh/id_rsa):   #1
Enter passphrase (empty for no passphrase):                        #2
Enter same passphrase again:                                       #3
```
\#1:如果不填,默认生成在`/home/username/.ssh/id_rsa` 中,即用户家的目录下.公钥文件名通常是`私钥文件名+.pub`.
\#2:填入密码使得每次登录时需要密码以登录.
\#3:确认\#2密码.

### 首次 ssh 登录服务器
1.上传__公钥__至服务器:  
`创建秘钥`:输入`.ssh/.pub` 文件中的密码
`绑定/解绑云主机`:绑定你的服务器(需要在关机下执行)
![](https://ws2.sinaimg.cn/large/006tNc79gy1fpp0gvgd8xj30rm044gli.jpg)

2.登录:  
命令:`shh username@server_ip`  
第一次登录可能会显示

```
~ ssh username@server_ip
The authenticity of host 'server_ip (server_ip)' can't be established.
ECDSA key fingerprint is SHA256:61U/SJ4n/QdR7oKT2gaHNuGxhx98saqMfzJnzA1XFZg.
Are you sure you want to continue connecting (yes/no)?
```

3.登陆成功:  

```
Last login: Sun Mar 25 13:07:24 2018 from client_ip
[root@VM_0_7_centos ~]#
```

__ssh 登录流程解析__

```
密钥登录比密码登录安全，主要是因为他使用了非对称加密，登录过程中需要用到密钥对。整个登录流程如下：

1.远程服务器持有公钥，当有用户进行登录，服务器就会随机生成一串字符串，然后发送给正在进行登录的用户。
2.用户收到远程服务器发来的字符串，使用与远程服务器公钥配对的私钥对字符串进行加密，再发送给远程服务器。
3.服务器使用公钥对用户发来的加密字符串进行解密，得到的解密字符串如果与第一步中发送给客户端的随机字符串一样，那么判断为登录成功。
```