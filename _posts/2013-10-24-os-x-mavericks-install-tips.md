---
layout: post
title: "安装OS X Mavericks 10.9的那些坑"
description: ""
category: 
tags: []
---

##安装时间
我是从Mac App Store下载升级的，安装全程大概要40分钟的时间（据说有的朋友反馈即使SSD也要这么久）。不要指望在几分钟内升级完成，最好在升级开始之后找点别的事情干。

##安装之后
为了能够正常使用和开发，我做了以下几件事：

1. 到App Store更新Xcode。更新完成后打开Xcode会提示需要安装额外组件，选安装。
2. 安装命令行工具。在终端中输入下面命令：  
```
$xcode-select --install 
```
3.  更新homebrew，输入下面命令：  

```
$brew update
$brew upgrade
```

4. ![assist](http://ww4.sinaimg.cn/large/70dcc3a2gw1e9w5o2frlzj20ik0cz0tm.jpg)
为了使用Moom、EVE等APP，开启辅助功能设置。位于系统偏好设置 - 安全性与隐私 - 隐私 标签页 - 左侧 辅助功能，在左下角点锁图标解锁之后，勾上你要使用的APP。
[来源](http://www.tekrevue.com/2013/06/25/how-to-enable-access-for-assistive-devices-in-os-x-mavericks/)
5. QQ更新到3.0.0以上，如果QQ的截图不能使用，可以使用系统提供的『抓图』工具，位于系统的『其他』文件夹里。也可以通过Alfred或Spotlight搜索『抓图』打开，平时可以固定在Dock上，随时调用。用这个工具截图后的图片可以直接Cmd+C复制，再粘贴到QQ中发送，也可以直接保存成文件。
6. MPlayerX更新到1.0.18版，否则无法使用。是的，万年不更新的MPlayerX居然昨天更新了！到[官网下载](http://mplayerx.org/download.html)可以找到这个版本。

##开始使用
还不了解OS X Mavericks带来了什么新东西？推荐看看官方给出的中文介绍：

1. 这篇比较详细：[](http://www.apple.com/cn/osx/whats-new/)。其中注意关于Safari 7.0的介绍，可以点击『了解更多』到[专门的页面](http://www.apple.com/cn/safari/)。
2. 这篇针对从OS X Mountain Lion升级过来的用户，每个功能有动画演示：[](https://help.apple.com/osx-mavericks/whats-new-from-mountain-lion)

还有什么坑我没提到的，欢迎在评论中提出，我会补充到文章里。
