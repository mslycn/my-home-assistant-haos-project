5.Docker daemon

dns nameserver

# linux

更换为公共DNS（如Google的 8.8.8.8 或国内 114.114.114.114）

# 配置全部容器的DNS

可以在/etc/docker/daemon.json文件中增加以下内容来设置。
~~~

{
	"dns" : [
		"114.114.114.114",
		"8.8.8.8",
		"8.8.4.4"
	]
}
~~~

这样每次启动的容器 DNS 自动配置为 114.114.114.114 和 8.8.8.8


# 配置docker内部的/etc/hosts

## Docker 会默认用主机上的 /etc/resolv.conf 来配置容器。

docker daemon会copy缩主机的/etc/resolv.conf，然后对该copy进行处理（将那些/etc/resolv.conf中ping不通的nameserver项给抛弃）,处理完成后留下的部分就作为该容器内部的/etc/resolv.conf。


容器内的/etc/resolv.conf改动后，不再关联缩主机的/etc/resolv.conf，不管这种改动是在容器中手动改动了/etc/resolv.conf文件，还是通过 --dns, --dns-search, or --dns-opt启动时改动（实际上系统启动时自动修改了容器内的/etc/resolv.conf）

### Note
- 容器内嵌的DNS server
~~~
从Docker 1.10版本开始，docker daemon实现了一个容器内嵌的DNS server

Docker 1.2.0 开始支持在运行中的容器里直接编辑 /etc/resolv.conf 、/etc/hostname、/etc/hosts。 这些修改是临时的，只在运行的容器中保留，容器终止或重启并不会被保存下来。也不会被docker commit提交。
~~~

## 容器内的DNS配置文件

Docker 1.2.0 开始支持在运行中的容器里直接编辑 /etc/resolv.conf 、/etc/hostname、/etc/hosts。
这些修改是临时的，只在运行的容器中保留，容器终止或重启并不会被保存下来。也不会被docker commit提交。

                        
原文链接：https://blog.csdn.net/m0_45406092/article/details/105299138
~~~
root@raspberrypi:~# docker exec -it ha sh
/config # cat /etc/resolv.conf
~~~

/etc/resolv.conf 默认与主机上的 /etc/resolv.conf一致

/config # cat /etc/resolv.conf
~~~
# Generated by Docker Engine.
# This file can be edited; Docker Engine will not make further changes once it
# has been modified.

nameserver 192.168.1.1
nameserver 192.168.2.1
nameserver fd00::d29f

# Based on host file: '/etc/resolv.conf'
# Overrides: []

~~~

/etc/hostname 容器的主机名
~~~
/config # cat /etc/hostname
raspberrypi

~~~



## docker run 命令启动容器时通过参数指定修改配置

如果用户想要手动指定容器的配置，可以在使用 docker run 命令启动容器时加入如下参数：

-h HOSTNAME 或者 --hostname=HOSTNAME 设定容器的主机名，它会被写到容器内的 /etc/hostname 和 /etc/hosts。但它在容器外部看不到，既不会在 docker container ls 中显示，也不会在其他的容器的 /etc/hosts 看到。

--dns=IP_ADDRESS 添加 DNS 服务器到容器的 /etc/resolv.conf 中，让容器用这个服务器来解析所有不在 /etc/hosts 中的主机名。

--dns-search=DOMAIN 设定容器的搜索域，当设定搜索域为 .example.com 时，在搜索一个名为 host 的主机时，DNS 不仅搜索 host，还会搜索 host.example.com。

## Docker 会默认用主机上的 /etc/resolv.conf 来配置容器。

docker daemon会将copy本主机的/etc/resolv.conf，然后对该copy进行处理（将那些/etc/resolv.conf中ping不通的nameserver项给抛弃）,处理完成后留下的部分就作为该容器内部的/etc/resolv.conf。

~~~
1 如果docker run时不含 --dns=IP_ADDRESS…, --dns-search=DOMAIN…, or --dns-opt=OPTION…参数，docker daemon会将copy本主机的/etc/resolv.conf，然后对该copy进行处理（将那些/etc/resolv.conf中ping不通的nameserver项给抛弃）,处理完成后留下的部分就作为该容器内部的/etc/resolv.conf。

因此，如果你想利用宿主机中的/etc/resolv.conf配置的nameserver进行域名解析，那么你需要在宿主机中该dns service配置一个宿主机内容器能ping通的IP。
2 注意容器内/etc/resolv.conf中配置的DNS server，只有当内置DNS server无法解析某个name时，才会用到。
~~~


配置全部容器的DNS
可以在/etc/docker/daemon.json文件中增加以下内容来设置。
~~~
{
	"dns" : [
		"114.114.114.114",
		"8.8.8.8"
	]
}
~~~

经检查，hassos 的/etc/docker/daemon.json文件中，默认已配置断点续传，无需添加。


