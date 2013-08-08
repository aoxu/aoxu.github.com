---
layout: post
title: "在iTerm2中使用Alt+F和Alt+B快捷键"
description: ""
category: 
tags: []
---
##Alt+F和Alt+B的作用
Linux用户知道，在Linux命令行下用 Alt+F 和 Alt+B 可以按词一个个往前、后移动光标。例如下面这个命令

```zsh
$ps aux | grep ssh
```
输入完这条命令，光标在末尾。按一次 Alt+B ，光标会移动到ssh的前面；再按一次Alt+B，光标会移动到grep的前面；按一次Alt+F，光标会移动到grep的后面。
用这个快捷键可以方便地修改一条命令。

##Mac OS X下的终端问题
我使用的OS X版本是10.8 Mountain Lion，无论是系统自带终端Terminal.app，还是[iTerm2.app](http://www.iterm2.com/)，都不支持Alt+F和Alt+B快捷键。如果按下option+F，会输入一个很像f的字符，如下：

```
ƒ
```
这样就无法使用这个快捷键。

##解决办法
如果什么都不改动，可以使用option+←和option+→来代替Alt+B和Alt+F，达到相同的效果。

我们还能修改iTerm2的设置来正常使用这个快捷键。方法是：
1. 打开菜单iTerm - Preferences，选择Profiles标签页，再点到Keys选项。
2. 在Profile Shortcut Keys(快捷键映射列表)下面点+按钮，新增两个快捷键。
3. 第一个快捷键：在Keyboard Shortcut按下option+F，Action选择Send Hex Code，最后在输入框输入下面内容

```
0x1b 0x1b 0x5b 0x43
```
4. 第二个快捷键：在Keyboard Shortcut按下option+B，Action选择Send Hex Code，最后在输入框输入下面内容

```
0x1b 0x1b 0x5b 0x44
```
然后就可以用option+F和option+B来移动光标了。
