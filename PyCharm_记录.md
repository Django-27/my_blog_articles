### 利用PyCharm的Deployment功能映射本地代码和远程代码
    tools -> Deployment -> Configuration
          -> +用户 -> SFTP -> host地址和端口,如127.0.0.1:2200 -> 用户和密码
          -> Mapping -> local path 和 服务器path , 完成代码映射
    tools -> Deployment -> Options -> On explicit save action(Ctrl-s即自动上传)
    tools -> Deployment -> browse remote host侧边栏查看远程目录
    tools -> start ssh session (setting ssh Terminal-> Default encoding:UTF-8)
### 利用PyCharm远程调试
    本地编辑代码，扔到远端服务器上执行，然后debug结果本地显示
    File -> Setting -> Python Interpreter -> Add Remote -> SSH Credentials
         -> 主机IP，端口，用户名，密码

![image](http://note.youdao.com/yws/api/personal/file/FE86CB34401047868770B0A29E50EB11?method=download&shareKey=4d5da560ae1becef77852e616635ff91)

![image](http://note.youdao.com/yws/public/resource/9de657f6beaffa68f2619e3f1fa38098/xmlnote/510045101D4341A1A8E939712073F298/1087)


![image](http://note.youdao.com/yws/public/resource/9de657f6beaffa68f2619e3f1fa38098/xmlnote/C6ADFA00AD814755B0D8C0E3B4BDB8AE/1130)