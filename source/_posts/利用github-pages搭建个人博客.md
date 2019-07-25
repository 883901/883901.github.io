---
title: 利用github pages搭建个人博客
date: 2019-07-25 13:07:16
tags: github pages
categories: NEXT主题
---
一直想搭建一个博客系统，之前觉得wordpress挺好的，搭建了一个，搭建起来更新几篇文章后就不想更新了，感觉wordpress挺笨重繁琐的，最近一个星期都在找好用的博客系统，发现了hexo系统还可以搭在github pages上，立马来了兴趣，接连1个星期都在学习搭建并且使用好看的next主题，
<!-- more --> 
今天尝试下载分支源文件的时候发现next主题文件夹是空的，之前上传源文件并没有上传成功next主题，百度了半小时也没解决，就想着重新搭一次，反正 config 文件都有备份，然后就想着把搭建流程记下来为以后如果再搭建做参考！

## 安装前提
安装 Hexo 相当简单。然而在安装前，您必须检查电脑中是否已安装下列应用程序：
1.[Node.js](https://nodejs.org/en/)  (Should be at least nodejs 6.9)
2.[GIT](https://git-scm.com/) 安装git工具

## 安装hexo
```
npm install -g hexo-cli
```
安装 Hexo 完成后，请执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件。
```
hexo init <folder>
cd <folder>
npm install
```
新建完成后，指定文件夹的目录如下：
```
.
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes
```
_config.yml 是网站的配置信息，可以在此修改大部分的参数。重装的时候可以用备份的_config.yml直接代替。至此hexo安装完毕,以下是hexo命令：
```
hexo init [folder]      #新建一个网站。如果没有设置 folder ，Hexo 默认在目前的文件夹建立网站。
hexo new [layout] <title> #新建一篇文章。如果没有设置 layout 的话，默认使用 _config.yml 中的 default_layout 参数代替。默认为post文章。
hexo new "post title with whitespace"    #如果标题包含空格的话，请使用引号括起来。
hexo generate                            #生成静态文件。简写为：hexo g
hexo publish [layout] <filename>         #发表草稿。
hexo server                              #启动服务器（本地） 简写为： hexo s 
hexo deploy                              #简写为：hexo d  部署网站。后面加 -g, --generate 部署之前预先生成静态文件
hexo clean                               #清除缓存文件 (db.json) 和已生成的静态文件 (public)。 更改站点文件不生效时可能需要运行该命令。
hexo list <type>                         #列出网站资料
hexo new page [layout]                   #新建分类页
```

## 安装next主题
打开终端，切换到Hexo 站点根目录并克隆NexT 主题的最新主分支：
```
cd hexo
git clone https://github.com/theme-next/hexo-theme-next themes/next
```

## 启用NexT
与所有Hexo主题一样，下载后，打开站点配置文件，查找theme部分，并将其值更改为next（或其他主题目录名称）。
```
HEXO / _config.yml
THEME: Next
```
现在您已经安装了NexT主题，接下来我们将验证它是否已正确启用。在更改主题和验证主题之间，我们最好使用hexo clean清理Hexo的缓存。重装时利用备份的_config.yml替换即可。

## 主题美化 字数统计和阅读时长(网站底部/文章内):
1.首先安装插件:
```
npm install hexo-symbols-count-time --save
```
2.然后修改站点配置文件如下:
```
symbols_count_time:
	separated_meta: true   ＃显示属性名称,设为false后只显示图标和统计数字,不显示属性的文字
	item_text_post: true   ＃显示属性名称,设为false后只显示图标和统计数字,不显示属性的文字
	item_text_total: true ＃底部footer是否显示字数统计属性文字(如站点总字数,站点阅读时长 ≈ 1 分钟)
	awl: 4     ＃计算字数的一个设置,没设置过
	wpm: 275  ＃一分钟阅读的字数	
```

## 添加评论系统 Vanline
1.到[leancloud](https://leancloud.app) 注册账号并创建应用（应用名随便填）。
2.点击应用到存储页面创建Class,名称为:Counter权限为：无限制。
3.点开设置-》应用key，把里面的appid 和 appkey 填入主题配置文件中：
```
valine:
  enable: true # 为true时启用评论
  appid:  # 这里填写上面得到的APP ID   注意空一格再输入ID和key,
  appkey:  # 这里填写上面得到的APP KEY
  notify: false #  邮件通知
  verify: false # 验证码
  placeholder:  #评论框中预设的文字,随意填写
  avatar: mm # gravatar style 头像,采用gravatar头像,到http://cn.gravatar.com/了解
  guest_info: nick,mail,link # custom comment header 访客信息,显示在评论框上面,三者可随意选择或全选
  pageSize: 10 # pagination size 评论分页大小
  visitor: false #
```
## 添加打赏:
```
 reward:
 　　enable: true　＃开启
 　　comment: 坚持原创技术分享，您的支持将鼓励我继续创作！　＃图片上方显示的文本
 　　wechatpay: ＃图片地址
 　　alipay: ＃图片地址
```
## 文章加密访问
在　/blog/themes/next/layout/_partials/head/head.swig 文件中添加：
```
<script> 
 (function(){
        if('{{ page.password }}'){
            if (prompt('请输入文章密码') !== '{{ page.password }}'){
                alert('密码错误！');
                history.back();
            }
        }
    })();
</script>
```
在需要加密的文章的页面顶部(Front matter区域)加入 “password : 设置密码值”

## 博客添加搜索功能
1.安装插件
```
npm install hexo-generator-searchdb --save
```
2.修改主题配置文件：
```
local_search:
    enable: true
```

## 页面底部增加总访问量和总访问人数
1.到883901.github.io\themes\next\layout\_third-party\analytics\busuanzi-counter.swig busuanzi文件下面添加：
```
<span id="busuanzi_container_site_pv">本站总访问量<span id="busuanzi_value_site_pv"></span>次</span>
    <span class="post-meta-divider">|</span>
    <span id="busuanzi_container_site_uv">本站访客数<span id="busuanzi_value_site_uv"></span>人</span>
```
2.主题文件下修改：
```
busuanzi_count:
  enable: true
  total_visitors: true
  total_visitors_icon: 
  total_views: true
  total_views_icon: 
  post_views: true
  post_views_icon: eye
```



