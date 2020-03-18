---
title: Ayer中文说明
date: 2019-12-03 13:26:02
tags: ['技术']
id: ayer
categories: 技术
---

# 介绍

> [Ayer](https://github.com/Shen-Yu/hexo-theme-ayer) 是一个干净且优雅的Hexo主题，自带响应式，加载速度很快，该有的功能都有，可配置项也很多，非常适合作为你的博客主题，主题内还附送了6张精美的高清壁纸。欢迎使用和Star支持，如果你在使用过程中有任何疑问或者建议，欢迎联系我！如果你的博客采用了本主题，欢迎在下面评论区留下地址~

[Ayer](https://github.com/Shen-Yu/hexo-theme-ayer) 在马来语中是“水”的意思，在西班牙语中是“昨天”的意思。

![hexo-theme-ayer](https://i.loli.net/2019/12/03/SHPinIAclMX1Gra.png)

[GitHub地址](https://github.com/Shen-Yu/hexo-theme-ayer)

[国内镜像](https://gitee.com/shen-yu/hexo-theme-ayer)

[效果预览](https://shen-yu.gitee.io)

[中文说明](https://shen-yu.gitee.io/2019/ayer/)

<!-- more -->

# 特性

1. 干净且优雅，文章内容美观易读
1. 首页封面全屏平铺，扁平化设计，简洁又不失高大上
1. 响应式设计，博客在桌面端、平板、手机等设备上均能很好的展现
1. 首页封面和文案可以任意更换，主题内附送6张精美高清壁纸
1. 时间轴式的归档页
1. 侧边栏可以点击显示或隐藏
1. 支持文章置顶和文章打赏
1. 支持文章字数和阅读时长统计
1. 支持网易云音乐播放
1. 支持 `MathJax` 数学公式
1. `TOC` 目录在文章页悬浮，跳转更方便
1. 可设置阅读文章时做密码验证（[hexo-blog-encrypt](https://github.com/MikeCoder/hexo-blog-encrypt/blob/master/ReadMe.zh.md)）
1. [Valine](https://valine.js.org/)和[Gitalk](https://gitalk.github.io/)评论模块（推荐配合`leancloud`使用 `Valine`）
1. 集成了不蒜子、百度统计、Google Analytics、CNZZ等统计功能
1. 支持Github Ribbons


如果想体验手机端浏览效果，可以扫一下二维码：

![手机端效果](https://i.loli.net/2019/12/04/CaJ8bZnojg4GQEf.png) 


# 打赏

本主题完全开源且免费，目前由我一个人维护，如果你觉得主题不错，你可以选择继续白嫖，也可以选择适当打赏我，不在于金额多少，而是能让我更有动力去维护这个主题。打赏请备注说明，谢谢~

<div style="width:100%;text-align:center;font-weight:bold">
<span style="width:30%;display:inline-block">
微信
<img src="https://i.loli.net/2020/02/23/L8D1wNJ5S4zoa7R.png" alt="wechat" style="width:100%"></span>
<span style="width:30%;;display:inline-block">
支付宝
<img src="https://i.loli.net/2020/02/23/3i1KQmMUL6eSpNw.jpg" alt="alipay" style="width:100%"></span>
</div>

# 安装
``` bash
# 国内用户如果速度较慢，可以把github地址替换为：https://gitee.com/shen-yu/hexo-theme-ayer.git
git clone https://github.com/Shen-Yu/hexo-theme-ayer.git themes/ayer
```

# 修改

将博客根目录下的 `_config.yml` 里的 `theme` 值修改成 `ayer`

``` yml
theme: ayer
```

# 更新

``` bash
cd themes/ayer
git pull
```

# 主题配置

以下是ayer主题目录下的 `_config.yml`文件配置，请先确保你已经读过[Hexo文档](https://hexo.io/zh-cn/docs/)。如果你在配置过程中有问题，请先擅用 [搜索引擎](https://cn.bing.com)。如果你搜不到解决方法，你可以参考：[我的博客源码](https://gitee.com/shen-yu/shen-yu/tree/dev/)，按照我的一模一样配肯定是不会有问题的。如果对部分字体或颜色等有定制需求，请自行在css文件进行修改，主题本身已经很符合审美，自定义配置项也很多，不建议改得花里胡哨，过大的字体和库都会影响博客加载速度。如果还有问题或者建议，那么请在评论区给我留言~

``` yml
# 侧边栏菜单
menu:
  主页: /
  归档: /archives
  分类: /categories
  标签: /tags
  摄影: http://shenyu-vip.lofter.com
  旅行: /tags/旅行/
  关于我: /2019/about

# 站点次标题和打字动效
# https://github.com/mattboldt/typed.js
subtitle:
  enable: true  # 是否开启动效
  text: 面朝大海，春暖花开  # 显示的文字
  text2: 愿你一生努力，一生被爱   # 滚动播放，如果不需要可以留空
  text3: 想要的都拥有，得不到的都释怀  # 最多支持三段文字
  startDelay: 0   # 延迟时间
  typeSpeed: 200  # 打字速度
  loop: true  # 是否循环
  backSpeed: 100  # 回退速度
  showCursor: true  # 是否显示光标

# 网站图标和侧边栏logo
favicon: /favicon.ico
logo: /images/ayer-side.svg

# 封面配置
# enable-是否启用封面；path-封面背景图；logo-封面logo
cover:
  enable: true
  path: /images/cover1.jpg  # /source/images目录下附送多张精美壁纸，可任意更换
  logo: /images/ayer.svg  # 如果不要直接设置成false

# 页面顶部进度条  
progressBar: true

# 网易云音乐插件
music:
  enable: false
  # 播放器尺寸类型(1：小尺寸、2：大尺寸)
  type: 1
  id: 518895142  # 网易云分享的音乐ID(更换音乐请更改此配置项)
  autoPlay: true  # 是否开启自动播放

# 文章配置
# 文章太长，截断按钮文字(在需要截断的行增加此标记：<!--more-->)
excerpt_link: 阅读更多...
# 如果你嫌每篇文章手动加more标记比较麻烦，又不想在首页全文显示，可以把excerpt_all设置成true，这样首页只会显示文章归档
excerpt_all: false

# 是否开启文章分享按钮
share_enable: true
# 国内的社交平台(If you are not in China, maybe you prefer to set:false)
share_china: true
# 文章分享文字
share_text: 分享

# 分页文字
nav_text:
  page_prev: 上一页
  page_next: 下一页
  post_prev: 上一篇
  post_next: 下一篇

# 文章页是否显示目录
toc: true

# 文章中的图片是否支持点击放大
image_viewer: true

# https://github.com/willin/hexo-wordcount
# 是否开启字数统计(关闭请设置enable为false)
# 也可以单独在md文件里Front-matter设置`no_word_count: true`属性，来自定义关闭字数统计
word_count:
  enable: true
  # 只在文章详情显示(不在首页显示)
  only_article_visit: true

# 打赏
# 打赏type设定：0-关闭打赏； 1-文章对应的md文件里有reward:true属性，才有打赏； 2-默认开启所有文章均有打赏，如果有些文章你不需要，请在文章对应的md文件里设置no_reward:true
reward_type: 1
# 打赏wording
reward_wording: '请我喝杯咖啡吧~'
# 支付宝二维码图片地址，跟你设置logo的方式一样。比如：/images/alipay.jpg
alipay: /images/alipay.jpg
# 微信二维码图片地址
weixin: /images/wechat.jpg

# 版权声明
# 版权声明type设定：0-关闭版权声明； 1-文章对应的md文件里有copyright: true属性，才有版权声明； 2-所有文章均有版权声明
copyright_type: 2

# 是否启用搜索
search: true

# RSS订阅(先安装hexo-generator-feed插件，再去博客根目录config进行配置)
rss: /atom.xml

# 评论：1、Valine(推荐)；2、Gitalk

# 1、Valine[一款快速、简洁且高效的无后端评论系统](https://github.com/xCss/Valine)
# 启用Valine必须先创建leancloud应用， 注册账号后获取 id|key 填入即可
leancloud:  
  enable: true
  app_id: #
  app_key: #
# Valine配置(如果有些文章你想关闭评论，请在文章对应的md文件里设置no_valine:true)
valine:
  enable: true # 是否启用
  verify: false # 是否开启防垃圾评论验证
  notify: false # 是否开启邮件提醒(https://valine.js.org/notify.html)
  avatar: mp # 头像样式(https://valine.js.org/avatar.html)
  placeholder: 给我的文章加点评论吧~ # placeholder

# 2、Gitalk(https://github.com/gitalk/gitalk)
gitalk:
  enable: false # true
  clientID: # GitHub Application Client ID
  clientSecret: # Client Secret
  repo: # Repository name
  owner: # GitHub ID
  admin: # GitHub ID
  
# GitHub Ribbons-封面右上角的forkme
github: 
  # (关闭请设置为false)
  url: https://github.com/Shen-Yu/hexo-theme-ayer

# fancybox(仅用于相册展示，若需要可配置albums)
fancybox: true

# 访问量统计(不蒜子)
busuanzi:
  enable: true

# 友盟cnzz统计(url填js代码src链接)
cnzz:
  enable: true
  url: #

# Google Analytics
google_analytics: ''
# 百度统计
baidu_analytics: ''

# 数学公式
mathjax: true

# 网站成立年份(默认为 2019，若填入年份小于当前年份，则显示为 2018-2019 类似的格式)
since: 2019

#是否显示页脚信息(建议保留，有助于本主题的推广)
pageFooter: true

#ICP备案信息尾部显示
icp:
  enable: false
  url: 'http://www.beian.miit.gov.cn/' # 备案链接
  text: '浙ICP备88888888' # 备案信息
```


## 插件(必需)

+ [hexo-generator-searchdb](https://github.com/theme-next/hexo-generator-searchdb) 用于搜索
	
  ```yml
  npm install hexo-generator-searchdb --save
  ```
  然后将以下配置复制到你博客根目录下的 `_config.yml` 里（注意不是ayer目录下的）:
  
  ```yml
  # hexo-generator-searchdb
  search:
    path: search.xml
    field: post
    format: html
  ```

+ [hexo-generate-feed](https://github.com/hexojs/hexo-generator-feed) 用于生成RSS订阅

  ```yml
  npm install hexo-generator-feed --save
  ```
  
    然后将以下配置复制到你博客根目录下的 `_config.yml` 里（注意不是ayer目录下的）:
  
  ```yml
  feed:
      type: atom
      path: atom.xml
      limit: 20
      hub:
      content:
      content_limit: 140
      content_limit_delim: ' '
      order_by: -date	
  ```

## 插件(可选)

+ [hexo-generator-index-pin-top](https://github.com/netcan/hexo-generator-index-pin-top) 用于文章置顶

+ [hexo-blog-encrypt](https://github.com/MikeCoder/hexo-blog-encrypt/blob/master/ReadMe.zh.md) 用于文章加密

+ [hexo-tag-aplayer](https://github.com/MoePlayer/hexo-tag-aplayer/blob/master/docs/README-zh_cn.md) 用于播放音乐

+ [hexo-tag-dplayer](https://github.com/MoePlayer/hexo-tag-dplayer) 用于播放视频

+ [hexo-helper-live2d](https://github.com/EYHN/hexo-helper-live2d/blob/master/README.zh-CN.md) 二次元看板娘

更多插件请见 [hexo插件市场](https://hexo.io/plugins/)

## 分类
``` bash
  hexo new page categories
```
然后将以下复制到/source/categories/index.md文件
``` md
---
title: categories
type: "categories"
layout: "categories"
---
```

## 标签
``` bash
  hexo new page tags
```
配置同分类一样

## 相册
需要在文章顶部配置



``` md
---
title: Gallery

albums: [
        ["img_url","img_caption"],
        ["img_url","img_caption"]
        ]
---
```

## 文章目录

用Tocbot解析文章标题并生成目录

+ 将以下配置复制到你ayer目录下的 `_config.yml` 里：

	``` bash
	# Toc
  toc: true
	```
+ 当然你可能并不想所有文章都生成悬浮目录，你可以在文章顶部的配置中加一行来进行关闭：

	``` md
  ---
  toc: false
  ---
	```

---

# 常见问题

## 一.本地图片引用了却无法显示

> 插入图片的两种方法：1.引用图床，2.引用本地图片。为了防止路径出错，建议使用图床。

### 1.图床
推荐使用：[SM.MS](https://sm.ms/)，[聚合图床](https://www.superbed.cn/)

### 2.本地图片
建议在hexo创建的博客目录下的source中建立一个images文件夹专门放图片，路径：你的博客目录`/source/images`，如果还是无法显示，请尝试在文章里用html的img标签来引用本地图片。


## 二.点击侧边栏页面无法显示

原因：ayer主题目录下的 `config.yml` 里menu属性的路径不对，这需要你根据页面路径手动配置。

以我的博客为例：

```yaml
menu:
  主页: /
  归档: /archives
  分类: /categories
  标签: /tags
  旅行: /tags/旅行/
  摄影: http://shenyu-vip.lofter.com
  关于我: /2019/about
```

上面的`归档/archives`是固定的，你不需要修改，`标签`和`分类`都需要手动创建目录，`旅行`实际上就是一个标签页，当你在文章头部设置tags属性后就会自动生成，`摄影`是一个站外的绝对路径，`关于我`实际上就是一个正常的文章页。好了，现在一个侧边栏导航就已经配置好了。

## 三.为什么修改了配置却没有效果

建议每次生成站点或部署之前都用 `hexo clean` 命令清理一下缓存，另外你可能还需要刷新一下。

## 四.怎么修改大标题和站点信息

站点配置文件`_config.yml`是hexo站点根目录下的主配置文件(还不知道是哪里的，自己google)，注意：别和`ayer`主题目录下的`_config.yml`搞混了。

修改网站各种资料，例如标题、副标题和邮箱等个人资料，请修改站点根目录下的`_config.yml`

以我的博客为例：
![](https://i.loli.net/2020/02/26/On1VwGp9UXYbfa4.png)

## 五.怎么添加百度或谷歌统计

### 百度统计

在ayer的config配置里的`baidu_analytics`填上百度统计代码中的hm.js问好后面那一串东西

### 谷歌统计

在ayer的config配置里的`google_analytics`填上谷歌统计代码的跟踪ID，即UA值(包含UA)
