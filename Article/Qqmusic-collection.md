# Q音收藏数及其他音乐平台数据抓取介绍

去年《我们的歌第二季》播出期间，我做了一个节目音源相关数据的汇总页面发在了豆瓣。最近不知为何，这个贴子又被顶上来了，也有不少朋友豆油我咨询接口相关的问题。所以我在这里整理一下给大家做个参考。

先放上原豆瓣贴子的地址，具体说明和链接都写在里面了：

[【数据】为我们的歌第二季开一个数据站｜更新Q音收藏数](https://www.douban.com/group/topic/198745110/)

具体的操作过程我不会一步一步写得那么详细，只是大概梳理一下做这个Page的整个思路，以及里面列出的另一个页面 [Joey音乐榜单](https://prettycrazyjoey.cn/rank) 中的其他平台（用到的Libary或Public Api申请地址等等）的汇总和整理。

## 第一步，明确你想要的内容

首先，要知道怎么抓包

比较常用的抓包工具 `fiddler` `Charles` 等等，网上搜关键字 *xxx抓包教程* 能搜到一大把，所以我就不在这里细说了。这类抓包工具的主要功能是可以捕捉到你在网页或app上每个操作而发起的http请求，这样你可以知道你到达的每个页面，分别请求了哪些接口，那些接口返回的数据是对你有用的。接下来你就可以不依赖于浏览器或app去单独发起这些请求，获取你想要的数据。

## 第二步，模拟请求


## 第三步，用代码实现


## 第四步，让数据更友好得展示出来


## 补充：其他音乐平台开发资源整理