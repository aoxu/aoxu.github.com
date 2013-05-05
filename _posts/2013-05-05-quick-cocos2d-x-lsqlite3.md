---
layout: post
title: "在quick-cocos2d-x引擎中集成lua的sqlite支持"
description: ""
category: 
tags: []
---
##quick-cocos2d-x框架
下面是原作者[dualface](http://dualface.github.io/)写的一段介绍：  
> [quick-cocos2d-x](https://github.com/dualface/quick-cocos2d-x) 是一个可以让您觉得“爽快”的 cocos2d-x 的扩展版。基于 [cocos2d-x](http://www.cocos2d-x.org/)，完全的跨平台能力、优异的性能和可靠性。而 quick-cocos2d-x 在这一切的基础上，添加了完善的 Lua 脚本语言支持，让开发者可以使用 Lua 这种简单易用的脚本语言完成商业品质的移动游戏。  

主要特点就是可以用Lua来做iOS游戏，虽然原版的cocos2d-x也支持用Lua开发，但是这个扩展版的框架整合了各种针对Lua的改进。quick-cocos2d-x精简了原来的多平台支持，支持iOS/Android平台的游戏开发，而且开发者可以在Mac/Windows上写代码、调试。本文仅关注在Mac上做iOS游戏的开发。  

写这篇文章时，这个框架依然处在开发中，没有完全达到它想要实现的目标。这个框架是100%开源的，这意味着：  
1. 即使没有完成，依然比原版的cocos2d-x更丰富，不满意的地方可以自己修改。  
2. 我会参与到这个框架的代码贡献，帮助dualface一起完善这个框架。  

##框架的安装和使用
###安装
由于现在还没有准备好kickstart包（Mac模拟器还没有完成），所以只能从源码安装。参照[项目主页的说明](https://github.com/dualface/quick-cocos2d-x#build-from-sources)，其中第1步的`Get soruces from Github.com`会比较慢，因为代码库的历史记录比较多，尤其是里面引用的[cocos2d-x子模块](https://github.com/dualface/cocos2d-x)比较大，整个拷贝下来>500MB。有2种办法可以快速下载：  

1. 直接在项目主页左上角下载ZIP文件。  
ZIP文件只包含master主干最新版的文件，但是不包含子模块，子模块也需要单独下载。  
2. 使用git的浅clone，指定clone的深度。
{% highlight bash %}
git clone --depth 1 git://github.com/dualface/quick-cocos2d-x.git
cd quick-cocos2d-x
git clone --depth 1 git@github.com:dualface/cocos2d-x.git lib/cocos2d-x
git submodule add git@github.com:dualface/cocos2d-x.git lib/cocos2d-x
{% endhighlight %}
这个方法适用于所有的git项目。  

后面照着主页的说明做就可以了。
###cocos2d-x子模块
由于quick-cocos2d-x使用了修改版的cocos2d-x，所以注意不需要使用官方版的cocos2d-x，也不必下载官方版的cocos2d-x。  
已经安装了官方版cocos2d-x的也没有影响，两者可以并存。

##初次使用
###运行示例
用Xcode打开示例项目：  
`quick-cocos2d-x/samples/CoinFlip/proj.ios/CoinFlip.ios.xcodeproj`  
如果可以正常Run起来，看到如下的游戏界面，就说明开发环境已经搭建成功了。  
![CoinFlip.png](http://ww4.sinaimg.cn/large/a74ecc4cjw1e4dcckv6ioj20a30jpwgh.png)
###Hello, world!
打开`samples/CoinFlip/scrips/main.lua`
这个简短的lua源文件里，下面这一段是执行Lua代码的起始处：
<pre><code>
xpcall(function()
    require("game")
    game.startup()
end, __G__TRACKBACK__)
</code></pre>
改成
<pre><code>
xpcall(function()
    print("Hello, world!")
end, __G__TRACKBACK__)
</code></pre>
你将会在控制台里看到这一句输出。  
![HelloWorld.png](http://ww1.sinaimg.cn/large/a74eed94jw1e4dds45upoj205w0373yn.png)  

##为Lua集成sqlite
###luaSqlite3和sqlite库
客户端跨平台数据存储的最佳方案是使用sqlite3，为了把sqlite3的操作集成到quick-cocos2d-x上，给Lua调用，需要以下2个库：  

* [LuaSQLite3](http://lua.sqlite.org/index.cgi/doc/tip/doc/lsqlite3.wiki) version 0.9.1 稳定版  
  lsqlite3是名字的简称，第一个字母l代表lua，这是一个用C语言写的lua模块，提供lua语言的API. 这个模块依赖sqlite库.  
* [SQLite](http://www.sqlite.org/releaselog/3_7_16_2.html) version 3.7.16.2 稳定版

###集成方法
用Xcode打开`quick-cocos2d-x/lib/proj.ios/libquickcocos2dx.xcodeproj`，需要添加两个目录。  在`lib/lua_extensions/`下建好lsqlite3和sqlite两个目录，源码拷贝进去。然后自己写一个`lsqlite3.h`，提供luaopen的入口。代码如下：
<pre><code>
#ifndef __LSQLITE3_H__
#define __LSQLITE3_H__

#include "lauxlib.h"

LUALIB_API int luaopen_lsqlite3(lua_State *L);

#endif
</code></pre>
再编辑`lib/lua_extensions/lua_extensions.c`文件，找到`luax_exts`，加入lsqlite3模块：
<pre><code>
static luaL_Reg luax_exts[] = {
    {"cjson", luaopen_cjson},
    {"zlib", luaopen_zlib},
    {"socket.core", luaopen_socket_core},
    {"mime.core", luaopen_mime_core},
    {"lsqlite3", luaopen_lsqlite3},  --添加本行代码

    {NULL, NULL}
};
</code></pre>
这些做完以后，你改动的文件结构应该是这样：  
![ChangeList.png](http://ww1.sinaimg.cn/large/a74e55b4jw1e4dfdolv8xj208g0743z9.png)  
其中VERSION文件是我自己写的，为了记录所使用sqlite库版本号。
###测试代码
在刚才写Hello, world!的地方，改成以下代码，就可以在quick-cocos2d-x中测试lua对sqlite的调用了。
<pre><code>
local sqlite3 = require("lsqlite3")

local db = sqlite3.open_memory()

db:exec[[
  CREATE TABLE test (id INTEGER PRIMARY KEY, content);

  INSERT INTO test VALUES (NULL, 'Hello World');
  INSERT INTO test VALUES (NULL, 'Hello Lua');
  INSERT INTO test VALUES (NULL, 'Hello Sqlite3')
]]

for row in db:nrows("SELECT * FROM test") do
    print(row.id, row.content)
end
</code></pre>
如果成功你将会在控制台看到三行文字输出：
<pre><code>
Hello World
Hello Lua
Hello Sqlite3
</code></pre>
相关的集成代码我已经[提交了pull request到quick-cocos2d-x](https://github.com/dualface/quick-cocos2d-x/pull/36)。