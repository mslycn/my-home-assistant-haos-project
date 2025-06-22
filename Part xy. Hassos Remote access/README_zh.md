# hassos 远程访问方案汇总

## IPv6 直连方案

通过 [IPv6地址]:8123 访问


## 方案一：内网穿透方案
IPv6 DDNS
ddns-go addon

Duck DNS addon

cpolar addon

生成 https://xxx.cpolar.io 访问


##  方案二：异地组网方案
ZeroTier或者Tailscale
在【配置】-【加载项】-【加载项商店】中有这两个应用，安装后将手机以及HomeAssistant接入到相应的ID内即可。

ZeroTier One addon


## Cloudflare DNS + Argo Tunnel

cloudflared tunnel --url http://hassio.local:8123 --hostname ha.cloudflare.com

