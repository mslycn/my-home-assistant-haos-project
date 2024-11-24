


nmcli is not available with the official add-on “Terminal & SSH”

nmcli is available with the HAC Add-on “SSH & Web Terminal”



## 原理
Hassos  通过 package_xxx_index.json 文件管理Addon 版本。在 github 官方项目官站可下载到Addon的包管理文件 package_gg_index.json。该文件中指定了所有依赖文件的地址，Hassos 依赖这些地址自动下载各种软件，并会先存放在（以Windows 为例） ~\Arduino15\staging\packages 目录，然后启动安装过程。

## 离线安装
离线安装 Hassos  第3方开发Addon的原理是：事先按照 package_esp32_index.json 文件所给的地址通过其它渠道下载好所需文件存放在特定目录，再启动 Arduino 激活安装过程。

## 关于版本
不同的 esp32 支持包的版本所依赖的其它包并不完全相同。只有在 Arduino IDE 的 Preference 中附加网址更新信息后，再打开开发板管理器，才可能找到 ESP32 安装包，并选择所需版本。

已下载和安装的版本如下，它们的副本都备份在本地“专业软件”目录下。

2.0.10

2.0.9 https://mirrors.sdu.edu.cn/github-release/espressif_arduino-esp32/2.0.10/package_esp32_dev_index.json

## 具体步骤

下载 Arduino 所必须的 Package 描述文件 package_esp32_index.json。放到 用户文件夹 \AppData\Local\Arduino15\下，如果没有相关文件夹请自行建立

下载 esp32-版本号.zip，注意版本号要正确。

下载所需的支持包，全部放入 ~\Arduino15\staging\packages 。注意：和自己的开发板无关的开发包不用管，这样可以节省时间。

打开 Arduino 附加开发板管理器网址。Arduino IDE>文件>首选项>附加开发板管理器网址中加入开发板包地址: https://dl.espressif.com/dl/package_esp32_index.json

安装开发板软件包：Arduino IDE>开发板>开发板管理器>esp32>安装









