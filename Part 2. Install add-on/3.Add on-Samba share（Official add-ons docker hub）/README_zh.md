## Install Add on-Samba share（Official add-ons）

Add on-samba进入HA配置目录
https://www.home-assistant.io/common-tasks/os/# 

## installing-and-using-the-samba-add-on
~~~
安装samba Add on（本文选用）
点击“配置”-“加载项、备份与 Supervisor”，右下角“加载项商店”，搜索“Samba”
~~~

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