ssh - 1.Add on-Terminal & SSH

Official add-ons

image source:https://registry-1.docker.io/v2/

终端太难受了，而且是残废版，所以需要装个 ssh 插件

## installing

前往 HA 配置 -> 加载项 -> 右下角加载项商店，搜索 ssh, 点进搜索结果中的 Terminal & SSH , 点击安装

## how to use
安装后点击启动 , 并打开自启动和守护

此时已经可以通过 打开 WEB UI 按钮在浏览器连接终端了，连接 ssh 还需要继续配置

然后切到配置选项卡，配置 ssh 登录用的密钥 / 密码等信息，并配置 ssh 端口 (注意如果不配置，那么 ssh 端口默认是关闭的), 保存并重启后，即可使用配置的密钥 / 密码通过 ssh 软件连接到 HAOS 的终端了