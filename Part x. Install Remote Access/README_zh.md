## 方案一：IPv6 DDNS
这一部分我是依赖本地Ubuntu Server搭建的Nginx反向代理解决的，感兴趣的小朋友可以参考我之前的《从零开始使用Ubuntu Server搭建家用NAS服务器》系列，如果是群晖（已经在第三方套件内安装并使用DDNS-Go的情况下，直接在控制面板的登陆界面，找到反向代理，将反向代理的地址设置为HomeAssistant的本地访问地址。

##  方案二：ZeroTier或者Tailscale
在【配置】-【加载项】-【加载项商店】中有这两个应用，安装后将手机以及HomeAssistant接入到相应的ID内即可。

## 方案三：cpolar
官方文档：https://cpolar.com/docs#linux-system-installation-cpolar

在SSH中输入以下命令安装cpolar：

curl -L https://www.cpolar.com/static/downloads/install-release-cpolar.sh | sudo bash
登录cpolar官网后台，点击左侧的验证，查看自己的认证 token，复制其值。

回到SSH界面，输入：

~~~
cpolar authtoken xxxxxxx
cpolar tcp 8123
~~~
添加并启动服务：

~~~
sudo systemctl enable cpolar
sudo systemctl start cpolar
~~~
登录后台，查看隧道在线状态

https://dashboard.cpolar.com/status



