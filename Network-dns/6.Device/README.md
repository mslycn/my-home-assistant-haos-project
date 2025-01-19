ESPHOME无法正常显示节点在线状态

添加设备，正常配置后，节点可以正常工作，HA里也可以正常接入。
但是esphome上始终显示offline。esphome是docker部署的。

搜索了半天。找到以下信息。基本就是两个重点：1，docker 使用host模式；2，或者docker添加ESPHOME_DASHBOARD_USE_PING=true

~~~
I see this question here from time to time, so lets help someone.
ESPhome uses mDNS witch is a multicast protocol, multicast does not cross vlans.
You have 4 options:
Use a Firewall/Router that permits mDNS to cross vlans
Use Avahi reflector on a RPI connected to all vlans
On hass.io add the "status_use_ping=true"
On esphome docker dashboard use the env "ESPHOME_DASHBOARD_USE_PING=true"

~~~