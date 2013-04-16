---
layout: post
title: "使用XMPP协议收发新浪微博私信"
description: ""
category: 
tags: []
---
#基本概念
先科普一下，[XMPP](https://zh.wikipedia.org/zh/XMPP)是一个著名的开放式即时通信协议，以前也叫Jabber，Gtalk用的就是这个协议。在Mac OS X系统上，使用[Adium](http://adium.im/)这个支持多账号、多协议的即时通信软件，可以完美地兼容XMPP。新浪微博私信是提供XMPP服务的，接下来我就用Adium来演示新浪微博私信的配置方法。  

#设置步骤
1. 打开Adium菜单里的`偏好设置`，第一个标签页就是`账号`，点击左下角的+号按钮添加自己的新浪微博账号。填写方法是新浪微博账号加上@weibo.com。新浪微博账号里的`@`符号用`\40`代替。如果你的账号是`xxx@gmail.com`，那么这里填写的Jabber ID就是`xxx\40gmail.com@weibo.com`。密码填写你的微博密码。  如图：![weibo_account](http://ww1.sinaimg.cn/large/a74eed94jw1e3rqlhnlqnj.jpg)  
2. 切换到`选项`，填写XMPP服务器，是`xmpp.weibo.com`。  如图：![weibo_xmpp](http://ww4.sinaimg.cn/large/a74ecc4cjw1e3rql2iasdj.jpg)  
3. 添加账号成功之后，Adium会与服务器验证，可能会弹出一个提示框，问你是否继续。点继续，就可以了。如果你点显示证书，就会发现这里的证书是一个叫John Doe的人自签发的。建议微博以后还是去买个第三方签发的证书吧，这点钱应该还是有的吧。。。  
如图：![xmpp_cert](http://ww4.sinaimg.cn/large/bfadf3bejw1e3rqw29j6jj.jpg)  

#亮点
一旦有微博好友上线，并且你用的Mac Mountain Lion系统的话，Adium会调用系统的通知中心，在右上角弹出一个小通知。通过这个特性观察了一整天之后，才发现某些人微博上得还真是太频繁了，家住南山区的徐先生表示，从来没有见过这么无聊的人。（配图与文字无关）  
如图：![Aidum_notification](http://ww1.sinaimg.cn/large/a74ecc4cjw1e3rr4qctvej.jpg)

#暗点
如果你被这些通知弹烦了，可以在设置中关闭上线通知。  
如图：![notify_setting](http://ww2.sinaimg.cn/large/a74eed94jw1e3rrfe4759j.jpg)  

#Fin.