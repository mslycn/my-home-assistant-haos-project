
ha>network info


set hassos dns to 8.8.8.8

~~~
ha dns info
~~~

output
~~~
ha dns info
fallback: true
host: 172.30.32.3
llmnr: true
locals:
- dns://192.168.1.1
- dns://192.168.2.1
mdns: true
servers: []
update_available: false
version: 2025.02.0
version_latest: 2025.02.0

~~~


## How to change DNS setting in HassOS

home assistant cli:
~~~
ha dns options --servers dns://IP_ADDRESS
ha dns restart

~~~


## vi /etc/hosts

~~~

/config # cat /etc/hosts
127.0.0.1	localhost
::1		localhost ip6-localhost ip6-loopback
ff02::1		ip6-allnodes
ff02::2		ip6-allrouters

127.0.1.1		raspberrypi
185.199.108.133 raw.githubusercontent.com
140.82.114.4 github.com
~~~

Otherwise you will get:

ping github.com

~~~
No respone from github.com
~~~



Useful links

https://blog.csdn.net/gongchenyu/article/details/134675480 cn

https://github.com/home-assistant/operating-system/blob/dev/Documentation/network.md