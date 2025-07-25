# debian 12  + docker rpi p5b

Add enable_ipv6: true to all networks, if you didn’t define any networks.

# systemctl status NetworkManager
~~~
systemctl status NetworkManager
● NetworkManager.service - Network Manager
     Loaded: loaded (/lib/systemd/system/NetworkManager.service; enabled; preset: enabled)
     Active: active (running) since Sun 2025-05-18 03:24:49 CST; 3 days ago
       Docs: man:NetworkManager(8)
   Main PID: 666 (NetworkManager)
      Tasks: 3 (limit: 9585)
        CPU: 36.455s
     CGroup: /system.slice/NetworkManager.service
             └─666 /usr/sbin/NetworkManager --no-daemon

May 18 22:07:05 raspberrypi NetworkManager[666]: <info>  [1747577225.7905] device (br-caefea183540): carrier: link connected
May 19 02:21:33 raspberrypi NetworkManager[666]: <info>  [1747592493.5298] dhcp6 (eth0): state changed new lease, address=fd00::d29f::1000
May 19 07:05:37 raspberrypi NetworkManager[666]: <info>  [1747609537.5878] manager: (veth8613b62): new Veth device (/org/freedesktop/NetworkManager/Devices/13)
May 19 07:06:35 raspberrypi NetworkManager[666]: <info>  [1747609595.3993] manager: (vethf212d1a): new Veth device (/org/freedesktop/NetworkManager/Devices/14)
May 19 07:06:35 raspberrypi NetworkManager[666]: <info>  [1747609595.4227] device (vethf212d1a): carrier: link connected
May 19 07:06:35 raspberrypi NetworkManager[666]: <info>  [1747609595.4230] device (br-caefea183540): carrier: link connected
May 19 14:11:36 raspberrypi NetworkManager[666]: <info>  [1747635096.5924] dhcp6 (eth0): state changed new lease, address=fd00::d29f::1000
May 20 01:16:51 raspberrypi NetworkManager[666]: <info>  [1747675011.0430] dhcp6 (eth0): state changed new lease, address=fd00::d29f::1000
May 20 12:14:27 raspberrypi NetworkManager[666]: <info>  [1747714467.5322] dhcp6 (eth0): state changed new lease, address=fd00::d29f::1000
May 20 23:32:44 raspberrypi NetworkManager[666]: <info>  [1747755164.9582] dhcp6 (eth0): state changed new lease, address=fd00::d29f::1000

~~~

## 网络配置

检测有哪些网卡（物理网卡+虚拟网卡）

docker network ls

Hassos
~~~
NETWORK ID     NAME      DRIVER    SCOPE
012506a27536   bridge    bridge    local
04f9dd4db3c4   hassio    bridge    local
c2f07efe8983   host      host      local
074e19c5d2ef   none      null      local
~~~


~~~
# 编辑网络配置文件（有线）
sudo nano /etc/network/interfaces.d/eth0
# 添加静态IPv6配置（示例）
iface eth0 inet6 static
    address 2001:db8::1/64
    gateway 2001:db8::ff
~~~

重启网络服务：sudo systemctl restart networking

## 防火墙规则配置
~~~
# 允许IPv6转发
sudo ip6tables -A FORWARD -i eth0 -o docker0 -j ACCEPT
sudo ip6tables -A FORWARD -i docker0 -o eth0 -m state --state RELATED,ESTABLISHED -j ACCEPT
# NAT转换
sudo ip6tables -t nat -A POSTROUTING -s fd00::/64 -o eth0 -j MASQUERADE

~~~

Enable IP forwarding
~~~
echo 'net.ipv4.ip_forward = 1' | sudo tee -a /etc/sysctl.conf
echo 'net.ipv6.conf.all.forwarding = 1' | sudo tee -a /etc/sysctl.conf
sudo sysctl -p /etc/sysctl.conf

~~~


## mDNS配置
~~~
# 安装avahi-daemon实现.matter本地解析
sudo apt install avahi-daemon
sudo systemctl enable avahi-daemon

~~~


## test ping

~~~
root@raspberrypi:/data# ping -6 wwww.baidu.com
ping: wwww.baidu.com: Address family for hostname not supported
~~~

ping 与目录有关？

~~~
root@raspberrypi:~# ping -6 www.baidu.com
PING www.baidu.com(240e:ff:e020:99b:0:ff:b099:cff1) 56 data bytes
64 bytes from 240e:ff:e020:99b:0:ff:b099:cff1: icmp_seq=1 ttl=50 time=21.0 ms
64 bytes from 240e:ff:e020:99b:0:ff:b099:cff1: icmp_seq=2 ttl=50 time=21.2 ms

~~~

结果：
1. 与登录的账号有关。修改参数后，需ssh需重新登录rpi

2. 与路由器IPv6防火墙开启、关闭设置无关



## 检查关键节点

ip addr

ping6 raspberrypi.local

ping raspberrypi.local

/etc/sysctl.conf




