---
title: Nginx_记录
date:
tags:
---


 添加仓库 mate /etc/yum.repos.d/nginx.repo
进行编辑 [nginx]
         name=nginx repo
         baseurl=http://nginx.org/packages/mainline/centos/7/$basearch/
         gpgcheck=0
         enabled=1
安装 yum install nginx -y
启动 systemctl start nginx 
开启自启动 systemctl enable nginx  
ip addr
复制ip地址在浏览器中打开，可看到 头Welcome to Nginx. 

服务器
mkdir nginx
完成本地映射，既可以b实现服务器上的文件在本地编辑 sshfs root@192.163.33.11:/etc/nginx /Users/wanghao/desktop/nginx
本地使用atom编辑器打开 atom nginx
全局的设置是在nginx.conf文件下 
 
location /api {
    proxy_pass http://api.hello.dev;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
}
远程编辑文件：remote-atom (apple->setting->search) 
sudo curl -o /usr/local/bin/rmate https://github.com/aurora/rmate/blob/master/rmate
sudo chmod +x /usr/local/bin/rmate
ssh -R 52698:localhost:52698 vagrant@192.168.33.11
rmate hello.txt
同步本地与远程之间的文件：Remote-FTP
cd ~/desktop
mkdir app
cd app
atom ./
Packages -> Remote-FTP -> CreateSFTPconfigfile
