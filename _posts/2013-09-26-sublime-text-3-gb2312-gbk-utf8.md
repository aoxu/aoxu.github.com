---
layout: post
title: "Sublime Text 3技巧：支持GB2312和GBK编码"
description: ""
category: 
tags: []
---

##Sublime Text 3与Sublime Text 2的不同
其实有不少人写过如何让Sublime Text 2支持GB2312和GBK编码，[例如这篇](http://www.fuzhaopeng.com/2012/sublime-text-2-with-gb2312-gbk-support/)。基本原理就是先装好Package Control，然后再通过这个安装ConvertToUTF8的Package。但是文中的方法在Sublime Text 3时代行不通了，因为安装Package Control的方法发生了变化，[新的安装方法](https://sublime.wbond.net/installation)是，按`Control + ~`打开命令行，然后输入下面这一行代码：
```python
import urllib.request,os; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); open(os.path.join(ipp, pf), 'wb').write(urllib.request.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ','%20')).read())
```
执行之后，必须重启Sublime Text 3，才能继续下面的步骤。

##安装ConvertToUTF8
按`Command + Shift + P`打开万能搜索框，然后输入`install package`回车，这时候会加载所有的packges列表。看到列表之后再输入`ConvertToUTF8`回车，就会下载安装这个包了。装好之后会看到这个包的说明文件，如下图。
![ConvertToUTF8](http://ww2.sinaimg.cn/large/70dcc3a2gw1e909tgk2vjj20qm0l844b.jpg)

##可选安装GBK Encoding Support
ConvertToUTF8是用来把GB2312和GBK文件转换成UTF8编码的，作为一个程序员，使用UTF-8编码来保存是一个好习惯，尽量不要使用GB2312和GBK编码来写代码。  
如果有特殊需求——编辑之后必须以GB2312和GBK编码保存（例如淘宝的开发。。。），那么就照着上面的方法安装`GBK Encoding Support`这个包吧。

