成功安装Home Assistant的Add-On时遇到网络错误的问题 - dns


##  系统级别

操作系统级别

docker 服务级别

docker 单个容器级别


## 域名和域名系统两码事
域名(Domain Name)：是由一串用点分隔的名字组成的Internet上某一台计算机或计算机组的名称，用于在数据传输时标识计算机的电子方位(有时也指地理位置)。
域名的主要目的是方便人们记忆和输入，通过域名系统将域名翻译成可由计算机是被的IP地址，从而实现网络的互联。
 
域名系统：通常称作DNS，是Domain Name System的缩写，翻译成中文就是“域名系统”,DNS使用UDP端口53。
DNS是互联网中的一项核心服务，是用于实现域名和IP地址相互映射的一个分布式数据库，它将域名翻译成可由计算机识别的IP地址，使用户可以更快速便捷地访问互联。

域名系统服务器:


                        
原文链接：https://blog.csdn.net/cnzzs/article/details/145151202



DNS就是将域名映射成ip的分布式数据库服务器，它的作用如下图：

![这是图片](../img/Network-dns-3.jpg "Magic Gardens")

常用的DNS服务器

1、114.114.114.114

　　114.114.114.114是国内移动、电信和联通通用的DNS，手机和电脑端都可以使用，干净无广告，解析成功率相对来说更高，国内用户使用的比较多，而且速度相对快、稳定，是国内用户上网常用的DNS。

2、8.8.8.8

　　8.8.8.8是GOOGLE公司提供的DNS，该地址是全球通用的，相对来说，更适合国外以及访问国外网站的用户使用。

~~~
router的DNS->缩主机的DNS /etc/resolv.conf -> 全部容器的 DNS 可以在/etc/docker/daemon.json -> 容器内的/etc/resolv.conf改动(不再关联缩主机的/etc/resolv.conf)
~~~

2.缩主机的DNS /etc/resolv.conf

3.配置全部容器的DNS /etc/docker/daemon.json

配置全部容器的 DNS 可以在/etc/docker/daemon.json文件中增加以下内容来设置

4.配置容器内的DNS /etc/resolv.conf

容器内的/etc/resolv.conf改动后，不再关联缩主机的/etc/resolv.conf


### Docker容器实例中解析DNS的顺序
~~~
查找Docker daemon内置的DNS服务器127.0.0.11

查找docker run创建容器实例时通过 --dns参数（容器定制）设置的DNS服务器

查找Docker daemon通过 --dns参数，或/etc/docker/daemon.json(容器通用设置)文件设置的DNS服务器

查找Docker宿主机上/etc/resolv.conf文件中配置的DNS服务器

最后，查找Google的DNS服务器，如8.8.8.8和8.8.4.4，2001:4860:4860::8888和2001:4860:4860::8844
~~~
由近及远原则，内置服务器优先级最高，其次容器定制的，再其次容器通用的，最后是缩主机的dns，最最后是路由器的


HassOS使用nmcli设置静态IPv4地址
https://blog.csdn.net/gongchenyu/article/details/134675480

DNS records for huggingface.co
https://www.nslookup.io/domains/huggingface.co/dns-records/#authoritative

ha> ha network info 

output
~~~
                    
docker:
  address: 172.30.32.0/23
  dns: 172.30.32.3
  gateway: 172.30.32.1
  interface: hassio
host_internet: true
interfaces:
- connected: true
  enabled: true
  interface: enp2s4
  ipv4:
    address:
    - 192.168.2.119/24
    gateway: 192.168.2.1
    method: auto
    nameservers:
    - 192.168.1.1
    - 192.168.2.1
    ready: true
  ipv6:
    address:
    - fd18:f22c:7814:d900::1005/128
    - fd18:f22c:7814:d900:3461:9f3e:729e:9f94/64
    - fe80::f5d5:a437:c182:a251/64
    gateway: fe80::1af2:2cff:fe78:14d9
    method: auto
    nameservers:
    - fd18:f22c:7814:d900:1af2:2cff:fe78:14d9
    - '::'
    ready: true
  mac: 00:0C:
  primary: true
  type: ethernet
  vlan: null
  wifi: null
supervisor_internet: true



~~~


esphome addon

Tool Manager: Error: Please read https://bit.ly/package-manager-ioerror
ERROR Error: Please read https://bit.ly/package-manager-ioerror



关于在树莓派上安装Debian 12系统，配置Docker Matter服务器，并设置从路由器到Docker的IPv6网络。

需要先理清楚每个步骤的关键点。

step 1.树莓派安装Debian 12。

step 2.安装Docker。

step 3.配置Docker Matter server 和 docker otbr容器。Docker网络配置，需要创建自定义网络或使用桥接网络，并设置端口映射。

step 4.IPv6的配置。这里比较复杂，因为Docker默认不启用IPv6，需要手动配置。在daemon.json中启用IPv6，设置固定的IPv6子网，并配置iptables规则进行NAT转换。同时，宿主机本身需要支持IPv6，涉及到路由器的配置，在路由器上启用IPv6并分配前缀。此外，Docker网络需要配置为支持IPv6，可能需要创建自定义的IPv6网络，并确保容器分配到正确的IPv6地址。

网络拓扑方面，树莓派作为宿主机，需要正确配置网络接口。需要使用macvlan或ipvlan网络驱动，让Docker容器直接使用物理网络接口，或者通过NAT桥接。同时，路由器的DHCP设置可能需要调整，避免与Docker的IPv6子网冲突。

验证部分，需要检查Docker容器是否获取了IPv6地址，以及外部设备能否通过IPv6访问Matter服务。使用ip -6 addr查看容器IP，curl或ping6测试连通性。防火墙规则需要检查，确保ICMPv6和必要的端口开放。

可能遇到的问题包括IPv6地址分配失败、NAT规则未正确应用、防火墙阻止流量等。需要逐步排查，比如查看docker network inspect确认IPv6配置，检查iptables规则，以及测试网络连通性。

总结来说，整个过程涉及系统安装、Docker配置、Matter服务部署、IPv6网络设置以及网络调试。需要综合多个搜索结果中的步骤，并针对IPv6的特殊要求进行调整，确保各环节配置正确。