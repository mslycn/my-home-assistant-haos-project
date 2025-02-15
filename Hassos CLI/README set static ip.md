home-assistant-cli

How to set static ip address via nmcli 

Steps:
 - Go to the ha > login Panel.
 - Enter the 'login' menu.
 - Click on the Advanced SSH & Web Terminal add-on.
 - Set the 'Protection mode' switch to off.
 - Restart the add-on.

~~~


在x86机器上安装Home Assistant操作系统后,在ui更改了ip网关等数据后无法登录ha网页，通过ha CLI修改ip等数据

设备连接到显示器，显示如下

ha >

login 进入bash模式显示如下

#

输入以下命令进行操作

nmcli connection show列出您的连接

nmcli con show "Your Connection Name" 列出该连接的当前属性,如果知道需要编辑哪个可直接下一步进入编辑模式

nmcli con edit "Your Connection Name"进入该连接的编辑模式，此时屏幕显示一段提示语句外，命令行显示如下

nmcli>

print ipv4将向您显示该连接的 IPv4 属性

set ipv4.addresses you_ip 修改ipv4地址

set ipv4.gateway you_gateway 修改网关地址

set ..... 也可继续修改其他参数

save 保存

~~~
查看状态：systemctl status NetworkManager

sudo apt-get update
sudo apt-get -y install network-manager
~~~
