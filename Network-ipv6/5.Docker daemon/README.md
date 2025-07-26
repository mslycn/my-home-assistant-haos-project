# Enable  IPv6 support for Docker

The IPv6  is disable by default on Docker, you need to enable it by following steps

This will enable ipv6tables support for Docker,

/etc/docker/daemon.json
~~~
{
  "experimental": true,
  "ip6tables": true
}

~~~

sudo systemctl restart docker

detail：https://fariszr.com/docker-ipv6-setup-with-propagation/

修改 Docker 配置,开启容器的 IPv6 功能

以下配置会增加一段自定义内网 IPv6 地址，开启容器的 IPv6 功能，以及限制日志文件大小，防止 Docker 日志塞满硬盘 ：

这种方式是让 docker 默认的 bridge 网络启用 ipv6
~~~
cat > /etc/docker/daemon.json << EOF
{
    "log-driver": "json-file",
    "log-opts": {
        "max-size": "20m",
        "max-file": "3"
    },
    "ipv6": true,
    "fixed-cidr-v6": "fd00:dead:beef:c0::/80",
    "experimental":true,
    "ip6tables":true
}
~~~


systemctl restart docker

## 列出所有Docker网卡
docker network ls命令可以列出所有Docker网卡

docker network ls   （ha docker）

输出结果将包括网络ID、名称、驱动程序和范围信息
~~~
NETWORK ID     NAME                              DRIVER    SCOPE
2f1b2e62cc78   bridge                            bridge    local
c190f447be65   host                              host      local
4e4114b168fc   mosquitto_default                 bridge    local
f640f69d0fa6   none                              null      local
caefea183540   sherpa-onnx_default               bridge    local
e9bd32755d40   vosk_default                      bridge    local
95fd917067c9   wyoming-vosk-standalone_default   bridge    local

~~~


## 查docker 使用的网卡

查看特定网络的详细信息

docker network inspect host
~~~
docker network inspect host
[
    {
        "Name": "host",
        "Id": "c190f447be65f71760a5e7b322546f47e68877a9fa8bc73992c0e450dfe86306",
        "Created": "2025-04-25T07:50:12.159728098+08:00",
        "Scope": "local",
        "Driver": "host",
        "EnableIPv4": true,
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": null,


~~~

## 查看docker容器内部的网络配置

docker container inspect ha


##  docker容器内部的网络配置

使用docker exec命令进入容器，然后使用ifconfig或ip addr等命令查看网络配置

docker exec -it ha /bin/bash

命令将显示容器内的网络接口、IP地址等信息

/config # ping -6 www.baidu.com
PING www.baidu.com (240e:ff:e020:98c:0:ff:b061:c306): 56 data bytes
64 bytes from 240e:ff:e020:98c:0:ff:b061:c306: seq=0 ttl=50 time=22.558 ms
64 bytes from 240e:ff:e020:98c:0:ff:b061:c306: seq=1 ttl=50 time=22.610 ms
 

