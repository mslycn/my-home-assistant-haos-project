home-assistant-cli

ha> ha --help
~~~
  addons         Install, update, remove and configure Home Assistant add-ons
  audio          Audio device handling.
  authentication Authentication for Home Assistant users.
  cli            Get information, update or configure the Home Assistant cli backend
  core           Provides control of the Home Assistant Core
  dns            Get information, update or configure the Home Assistant DNS server
  docker         Docker backend specific for info and OCI configuration
  hardware       Provides hardware information about your system
  help           Help about any command
  host           Control the host/system that Home Assistant is running on
  info           Provides a general Home Assistant information overview
  multicast      Get information, update or configure the Home Assistant Multicast
  network        Network specific for updating, info and configuration imports
  observer       Get information, update or configure the Home Assistant observer
  os             Operating System specific for updating, info and configuration imports
  resolution     Resolution center of Supervisor, show issues and suggest solutions
  backups        Create, restore and remove backups
  supervisor     Monitor, control and configure the Home Assistant Supervisor

~~~

- 检查日志文件

ha> ha supervisor logs

ha> ha supervisor logs -f

output
~~~

~~~


docker ps
~~~
PROTECTION MODE ENABLED!

To be able to use this command, you'll need to disable
protection mode on this add-on. Without it, the add-on
is unable to access Docker.

Steps:
 - Go to the Settings Panel.
 - Enter the 'Add-ons' menu.
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



The things that really consume resources are add-ons, particularly Studio Code Server.

