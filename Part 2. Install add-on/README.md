


nmcli is not available with the official add-on “Terminal & SSH”

nmcli is available with the HAC Add-on “SSH & Web Terminal”



## 原理
Hassos  通过 package_xxx_index.json 文件管理Addon 版本。在 github 官方项目官站可下载到Addon的包管理文件 package_gg_index.json。该文件中指定了所有依赖文件的地址，Hassos 依赖这些地址自动下载各种软件，并会先存放在（以Windows 为例） ~\Arduino15\staging\packages 目录，然后启动安装过程。

## 离线安装
离线安装 Hassos  第3方开发Addon的原理是：事先按照 package_esp32_index.json 文件所给的地址通过其它渠道下载好所需文件存放在特定目录，再启动 Arduino 激活安装过程。



# Add-ons
先解决Add-ons按照源是否正常的问题。由3部分组成：官方、社区、（官方+社区）都没有的第3方 Add-on

Official Add-ons
...
Community Add-ons
...
Third Party Add-ons ->Add-ons Repositories
....

search esphome

output

~~~
在 Official add-ons 中未找到结果。
在 Home Assistant Community Add-ons 中未找到结果。

在 Frigate hass.io addons 中未找到结果。
在 HassOS Configurator 中未找到结果。
在 Matterbridge 中未找到结果。
在 Music Assistant 中未找到结果。
~~~

## Add-on - 常见问题

### 故障表现
我的add ons里面没多少插件可以安装,少一半

没有official add-ons，只有Home Assistant Community Add-ons

vm安装的os 只有社区仓库，官方仓库不显示，添加了官方仓库显示已存在

search "PiCorePlayer" Add-on
output
~~~
在 Official add-ons 中未找到结果。

在 ESPHome 中未找到结果。

在 Home Assistant Community Add-ons 中未找到结果。

在 Music Assistant 中未找到结果。
~~~
### 原因分析


### 解决办法

添加home assistant community add ons 源。需要网络环境

Step 1.启动高级模式（Advanced mode）

http://192.168.2.124:8123/profile/general

step 2.change DNS settings in hassOS
~~~
google dns：8.8.8.8
~~~

detail:http://localhost:4999/boards/topic/16771/add-ons-add-on#57814













