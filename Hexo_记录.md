---
title: Hexo_记录
date:
tags:
---


# 1 一定要以管理员权限进行hexo g -d
```
Error: fatal: AggregateException encountered.
   One or more errors occurred.
bash: /dev/tty: No such device or address
error: failed to execute prompt script (exit code 1)
fatal: could not read Username for 'https://github.com': No error

    at ChildProcess.<anonymous> (D:\Code\blog\node_modules\hexo-util\lib\spawn.js:37:17)

    at emitTwo (events.js:106:13)
    at ChildProcess.emit (events.js:194:7)
    at ChildProcess.cp.emit (D:\Code\blog\node_modules\cross-spawn\lib\enoent.js:40:29)
    at maybeClose (internal/child_process.js:899:16)
    at Socket.<anonymous> (internal/child_process.js:342:11)
    at emitOne (events.js:96:13)
    at Socket.emit (events.js:191:7)
    at Pipe._handle.close [as _onclose] (net.js:513:12)
```
### hexo g -d 其实这个错误与网络也有关系，有关系
github的主页分为项目主页和个人主页，其中项目主页的介绍[查看](https://pages.github.com/)。
- http://username.github.io/repository
- http://username.github.io

# 2 之后可以词用麦田音乐网的评论系统，挺喜欢
有一个好处是可以随时评论，评完即走，类似于微信小程序。应该是用的WordPress搭建，[源码](https://github.com/WordPress/WordPress/blob/master/wp-comments-post.php)。我还是比较喜欢这样的方式，简洁，相比较引入[多说](http://duoshuo.com/)的评论系统。还有Disqus评论。目前，hexo博客框架的官方next主题已经支持多说，Disqus，Hypercomments，网易云跟贴等多种第三方评议系统，但是官方的文档并没有对这部分的内容及时进行更新，所以广大朋友并不知道除了多说，disqus之外，其实还有很多可以进行选择的。
![image](http://note.youdao.com/yws/public/resource/9de657f6beaffa68f2619e3f1fa38098/xmlnote/7B3ABCA32D104F71B00D3D200C7A7E44/1859)


# 3 Adding ClustrMaps to your page footer
站点统计工具，统计ip地址，以图的形式展现[。clustrMaps](http://clustrmaps.com/)

# 4 初级阶段hexo的总结
![image](http://note.youdao.com/yws/public/resource/9de657f6beaffa68f2619e3f1fa38098/xmlnote/4DC9096193DF40A2BD975247BB42E966/1933)
- Git连接ssh： 设置Git的user name和email
```
git config --global user.name "aqiongbei" #改成你的注册Github的用户名
git config --global user.email "aqiongbei@gmail.com" #改成你的注册Github的邮箱
```
- Git连接ssh： 生成SSH密钥
```
ssh-keygen -t rsa -C "aqiongbei@gmail.com" #改成你注册Github的邮箱
```
- 添加密钥到 Github

```
点击自己的头像->settings->SSH Keys->Add SSH key
将本地 id_rsa.pub 中的内容粘贴到 Key 文本框中，随意输入一个 title，点击 Add Key 即可
```
- 测试Git
```
ssh -T git@github.com   # 或使用参数-vT，可以显示过程
```
- 安装hexo: npm install -g hexo-cli
- 新建一个网站: hexo init
- 添加一个文档: hexo new 'name'
- hexo clean | hexo g -d | hexo s -p 4000
- npm install hexo-deployer-git --save
# 5 npm安装hexo速度过慢

由于某些大家都知道的缘故，npm官方源在国内的下载速度极其慢，用官网的npm install hexo-cli -g速度非常感人，所以不推荐这种方式。这里我推荐用淘宝的npm分流——cnpm
安装过程很简单：
npm install -g cnpm --registry=https://registry.npm.taobao.org
然后等着装完即可，之后的用法和npm一样，无非是把npm install改成cnpm install,但是速度比之前快了不止一个数量级(不过下文为了方便理解，还是会用默认的npm安装，如果你发现速度不好的话，请自行替换成'cnpm')

# 6 更换主题 [yelee](https://github.com/MOxFIVE/hexo-theme-yelee)
