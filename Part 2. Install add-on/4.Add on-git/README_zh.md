Add on - git 进入HA配置目录

docker image source

https://registry-1.docker.io/v2/

## installing-and-using-the-git-add-on
~~~
安装samba Add on（本文选用）
点击“配置”-“加载项、备份与 Supervisor”，右下角“加载项商店”，搜索“git”
~~~

## configure

账号和密码

## how to use
~~~
访问HA配置目录
在windows系统---按Crtl+R----输入 \\HA主机IP
我的电脑-左边侧栏-Network-上面地址栏写 \\+ip
\\192.168.2.115
If you are on Windows you use \\<IP_ADDRESS>\, 
if you are on MacOS you use smb://<IP_ADDRESS> 
to connect to the shares.
输入Samba中设置的用户名和密码
options
虚拟机通过samba映射出来的都是homeassistant下的文件夹，看不到上一级
~~~